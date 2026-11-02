# Book collection behavior contract

Workshop sample: [book-app-project](../samples/book-app-project/README.md).
This contract preserves its existing behavior unless a correction is explicitly
approved. It is not permission to refactor or invent new validation requirements.

## Public interface and compatibility

- Keep `Book`, `BookCollection`, existing method signatures, and CLI commands.
- `Book` has `title`, `author`, `year`, and `read` fields; `read` defaults to `False`.
- Keep JSON persistence through the module-level `DATA_FILE`. Its default
  `data.json` path is relative to the working directory.
- Preserve existing pytest tests and sample data. Do not add a new framework,
  database, or public API as part of a structural refactor.

## Collection operations

- `add_book(title, author, year)` appends a `Book`, saves the collection, and
  returns that book, not a boolean. Duplicate titles are allowed.
- `list_books()` returns the current collection in stored order.
- `find_book_by_title(title)` uses exact case-insensitive matching with `lower()`
  and returns the first matching book or `None`.
- `find_by_author(author)` returns all exact case-insensitive author matches
  in collection order. It is not substring search.
- `mark_as_read(title)` marks only the first matching book, saves, and returns
  `True`; a missing title returns `False`.
- `remove_book(title)` removes only the first exact case-insensitive title
  match, saves, and returns `True`; a missing title returns `False`.

## Persistence and CLI

- Construction loads JSON records into `Book` objects. A missing file starts an
  empty collection. Malformed JSON prints the existing warning and starts empty;
  do not silently remove that warning or overwrite the input while loading.
- Saving writes the book fields as JSON with a closed file handle. Unexpected
  I/O or record-format errors must not be converted into success.
- Run the CLI from `samples/book-app-project`; `help` and `list` are read-only.
- Preserve one-based display numbering and the existing CLI command names.
- CLI inputs are stripped, and year text is converted to an integer. Empty year
  input currently becomes `0`; conversion failures are shown to the user.
- `utils.py` contains helpers not currently used by the CLI. Wiring them in or
  changing user messages must be part of the approved scope.

## Validation decisions

The sample has weak input validation. Report concrete consequences, but do not
invent a year range, reject blank values, trim model inputs, change search to
substring matching, or enforce title uniqueness without approval. If selected
findings need such a decision, record the exact accepted behavior in the plan
and update this contract before generating tests for that correction.

## Structural refactoring versus bug fixes

Extracting repeated code can preserve behavior. Changing validation, matching,
removal rules, persistence recovery, or CLI messages changes observable behavior.
The plan must declare those changes and receive user approval.
