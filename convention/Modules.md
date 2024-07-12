# Modules

##### Import

If the keyword `use` appears first in a file, comments and whitespace aside it is used as a module
import. If the string following starts `.` or `/` (mainly `./`, `../`, `/`) it is used as a path
import. This way you combine different files into one package. `use './lib.ü'`

If the string is a URL (or starts with `https://`, `http://`, `git://`), then it becomes a remote
module import. You will have to manually download these modules or let the package manager make it
for you. `use 'www.link-to-repo.com/path/to/.git'`

If the string starts with `@`, the following part is a preprocessor and handled with priority. Built-in
modules start with letters: `use 'stdlib'`

##### Export

All traits, types, trait implementations, constant values or static value references can be exported
with `pub`