# ![Builda Logo](https://raw.githubusercontent.com/spacenectar/builda/master/builda-logo.png)

## I have just set up this package, what now?

Congratulations! This package uses [Builda](https://builda.app) to generate the
project code and keep it up to date. The code is generated from the
['%PREFAB_NAME%' (v%PREFAB_VERSION%)](%PREFAB_URL%) prefab.

> [Learn about prefabs](https://builda.app/docs/prefabs)

Unlike other project generators, Builda is not a one-time thing. It will keep
your project up to date with the latest changes in the prefab.

Only the changes you specifically make to the project will be kept. This also helps
to keep codebase sizes small, as only files you make changes to need to be stored
in your repository.

## Getting started

The first thing you should do is to read the [documentation](http://builda.app/docs/getting-started/).
It will help you to understand how to use the package and how to customize it.

If you can't be bothered to read the documentation, there is a basic guide below
you can get started by running the following command:

```bash
npx builda init
```

This command will set up the project and generate the code. It will install all
the dependencies and set up the project for you. By the time it is done, you will
have a working project.

You can then run the project the same way you would run any other project:

e.g. for a Next.js project using `yarn`:

```bash
yarn dev
```

> **NOTE**: Builda can also be installed globally or ran via NPX. You don't really
> need to do this if you are running within an existing project, you just need
> to remember to prefix all `builda` commands with `yarn` or `npm run`.
> However if you want to use Builda to generate a new project, you will find life
> easier if you install it globally or use NPX.

## Where's all the code?

All of the code is still there. It's just hidden away in the .builda directory,
inside a special folder called 'export'. If it's not there, you can run
`builda build` to generate it but if you follow the instructions above, it will
be there already.

## How do I make changes?

You should not make changes to the code in the .builda directory as this code
will be overwritten when you run a `builda update` and in most cases, should not
be committed to your repository.

Instead, you should make changes to the code in the root directory. This is the
code that you will commit to your repository. Any file you add to the root
(other than ignored files - see below) will automatically synchronize with the
code in the .builda directory when you run `builda watch`
(see [Watch mode](#watch-mode) below).

### Updating existing files

If you want to update a file which already exists in the export directory, you
you can do this by running `builda eject <path>`. This will copy the file from
the export directory to the root directory. You can then make changes to the
file in the root directory and they will be synchronized with the export.

Fair warning though, any files you eject from the export directory will be
not receive any updates from the prefab.

> **NOTE**: A 'merge changes' command is planned for the future to help with
> this.

### Deleting existing files

If you want to delete a file which already exists in the export directory, you
you can do this by running `builda delete <path>`. This will add an entry to the
builda.json file in the `deleted_files` array and will delete the file from
the export directory. You can then commit the changes to the builda.json file
to your repository and this file will no longer be generated.

## Watch mode

Builda has a `watch` command which will look at the files in the project root
and update the code in the export directory when you make changes. If the prefab
this project was generated with was set up correctly, you should be able to
just run `yarn watch` or `npm run watch` otherwise you can run `yarn builda watch`.

By default, the `watch` command ignores the .builda directory and
[some other common files](https://builda.app/docs/watch#ignoring-files), but you
can add your own files to ignore by creating a `watch_ignore` entry in your
`builda.json` file.

> [Learn more about updating the builda config](https://builda.app/docs/configuration)

## Build mode

The `build` command will generate the code in the export directory. It will
also sync any files you have added to the root directory with the code in the
export directory. It is a one-shot command and will not watch for changes. This is
useful if you want to generate the code once and then run it or if you want to
generate the code in a CI/CD pipeline.
