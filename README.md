# V Documentation Generator

![Screenshot](./screenshot.png)

A [refactoring](Refactoring.md) of the official V documentation [generator](https://github.com/vlang/docs/tree/generator).

## External dependencies

You'll need V, of course.  Best to
[install it from source](https://github.com/vlang/v?tab=readme-ov-file#installing-v-from-source)
if you don't already have it.


## Contributing
To setup the generator and contribute changes to it, do this once:
```shell
git clone --branch generator https://github.com/vlang/docs docs_generator/
cd docs_generator/
v install
```
This will install all dependencies, and setup everything needed for you to generate
the documentation on your computer.


## Build the documentation
To build the documentation, after the setup, run the following commands:
```shell
v run .
```
This will download the latest version
of [docs.md](https://github.com/vlang/v/edit/master/doc/docs.md),
then it will regenerate the documentation from it, and save it in the `output`
directory.


## Testing the output
```shell
v -e 'import net.http.file; file.serve(folder: "output/")'
```
Now load http://localhost:4001/ in your browser.
