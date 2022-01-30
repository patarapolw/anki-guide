# Programming in Anki

I know about card creation and [tampering with the database](https://github.com/patarapolw/ankisync2). All of the methods are probably only done well on desktop OS's (Windows, macOS, Linux).

## CSV files

The obvious and best supported way is nonetheless, making CSV files, to create cards. You can also export notes to CSV files.

## AnkiConnect

[AnkiConnect](https://ankiweb.net/shared/info/2055492159) is a probably well-maintained and safe, although not really maintained by the Anki creator himself.

It works by exposing a web server on port 8765. I have had some issue on Windows with WSL 2, where Anki is a Windows app, and I tried to manipulate from WSL Linux.

AnkiConnect can also be slow, if you edit too many cards at once.

## APKG files

APKG files can be safely created by various projects, including [the one I have made a while ago](https://github.com/patarapolw/ankisync2). Essentially, APKG is a zip file composing of at least two files.

```
.
├── example
│   ├── example.anki2 # SQLite database
│   ├── media         # JSON file of Record<integer, filename>
│   ├── 1             # Media files with the names masked as integers
│   ├── 2
│   ├── 3
|   └── ...
└── example.apkg
```

If you understand the SQLite structure, you can edit it without problems.

APKG needs to be imported into Anki (desktop version) before it can be used.

## Internal Anki2 SQLite database

[It can be edited, at least up to version 2.1.26](https://github.com/patarapolw/ankisync2/issues/3), where the database structure remains the same as APKG. The database resides at `os.path.join(appdirs.user_data_dir('Anki2'), 'User 1', 'collection.anki2')`.

You should backup `collection.anki2` first, to avoid the risk of breaking the database.

## Anki2 SQLite database programming

It appears that you can create additional tables without issues. Some additional tables I would create includes Model, Deck, Template and Media, where Anki use in JSON form, and they cannot be easily indexed and edited using only SQLite.
