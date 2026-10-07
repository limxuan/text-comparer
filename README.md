# text-compare

Compare two text files and keep a history of every comparison.

## Quick start

```sh
./compare
```

With no arguments this diffs `fileA.txt` against `fileB.txt`.
Put your two files in the repo (or pass paths) and run it.
`fileA.txt` and `fileB.txt` are committed as empty placeholders; add your
text locally and it will not be tracked (they are marked `skip-worktree`).
`history/` is git-ignored.

```sh
./compare path/to/old.txt path/to/new.txt
```

Each run prints a short summary followed by the diff, for example:

```
  fileA.txt  ->  fileB.txt
  lines 3 -> 4   changes +2 -1   hunks 1   status: differ
  ------------------------------------------------------------

diff --git ...
-world
+there
```

## Options

| Flag | Description |
| --- | --- |
| `-n, --name NAME` | Label the comparison; used first in the saved filename |
| `-s, --side-by-side` | Side-by-side diff |
| `--color` / `--no-color` | Force / disable colored output |
| `-c, --context N` | Lines of context (default: 3) |
| `--no-save` | Print the diff without saving to `history/` |
| `--list` | List past comparisons |
| `--clean` | Delete the `history/` folder |
| `-h, --help` | Show help |

## History

Every run is written to `history/` as a plain, uncolored diff, e.g.:

```
history/20261007-153106-fileA.txt-vs-fileB.txt.diff
history/release-20261007-153231-fileA.txt-vs-fileB.txt.diff
```

Filenames are always timestamped, formatted as
`[<name>-]<timestamp>-<A>-vs-<B>.diff` — the name appears first when `-n`
is given. If a filename already exists, a `-1`, `-2`, ... suffix is added
so nothing is overwritten. Use `--no-save` to skip saving.

```sh
./compare -n release fileA.txt fileB.txt   # save with name + timestamp
./compare --list                           # show saved comparisons
./compare --clean                          # wipe history/
```

## Requirements

`bash` and `diff`. If `git` is installed it is used for colored output;
otherwise `diff -u` is used automatically.
