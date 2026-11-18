# Book Collection App

*(This README is intentionally rough so you can improve it with GitHub Copilot CLI)*

A Python app for managing books you have or want to read.
It can add, remove, and list books. Also mark them as read.

---

## Current Features

* Reads books from a JSON file (our database)
* Input checking is weak in some areas

---

## Files

* `book_app.py` - Main CLI entry point
* `books.py` - BookCollection class with data logic
* `utils.py` - Helper functions for UI and input
* `data.json` - Sample book data

---

## Running the App

```bash
python book_app.py list
python book_app.py add
python book_app.py find
python book_app.py remove
python book_app.py help
```

## Testing

No tests are bundled. Test generation and a testing framework are not required
for the current workshop modules.

---

## Notes

* Not production-ready (obviously)
* Some code could be improved
* Could add more commands later
