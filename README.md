# Dev Environment Tools

This is a collection of tools designed to help me set up and maintain my development environment. They're aimed primarily at being used on MacOS and on a laptop (although some are also handy on a desktop).

## env-switcher

[This project](env-switcher/) is a script to allow one to switch environment configuration between being on a corporate network/being at work vs being on a civilian network/being at home. At this moment it's particularly targeted at configuring maven settings.

You might ask, "Why use Node.js for this?" The short answer is that this was a good opportunity to start getting to learn the fundamentals of the ecosystem. This is also another way of saying: there are many improvements I can make to the script to make it more idiomatic.

### Installing

1. Clone this project to a location of your choosing.
2. Run `npm install` in the location where you installed the switcher. E.g. `/foo/bar/dev-env-tools/env-switcher`
3. Create and export an environment variable for the location of the the switcher. E.g. `export ENV_SWITCHER_HOME=/foo/bar/dev-env-tools/env-switcher`
4. Add to the PATH. E.g. `export PATH=$ENV_SWITCHER_HOME:$PATH`
5. Create a file named `settings.xml.civnet` which contains the maven settings file for when you're not on your corporate network/vpn. 
6. Create a file named `settings.xml.corpnet` which contains the maven settings file for when you're on your corporate network/vpn. 

### Running

By default, the script understands two parameter types: `civ` and `corp`. To run, simply:

```bash
$ envswitch civ
```

or

```bash
$ envswitch corp
```

## brew-app-finder

[This projects](brew-app-finder) is a script to allow ne to find the fully qualified path of an application installed by the [Homebrew](https://brew.sh) package manager.

You might ask, "Why use Node.js for this?" The short answer is that this was a good opportunity to start getting to learn the fundamentals of the ecosystem. This is also another way of saying: there are many improvements I can make to the script to make it more idiomatic.

### Installing

1. Clone this project to a location of your choosing.
2. Run `npm install` in the location where you installed the finder. E.g. `/foo/bar/dev-env-tools/brew-app-finder`

### Running 

Simply call the script. E.g.:

```bash
$ /foo/bar/dev-env-tools/brew-app-finder/findbrewapp maven
```

### Example

I use this command to allow me to configure CLI tools such as maven in my environment. 

```bash
export MAVEN_HOME=$(/foo/bar/dev-env-tools/brew-app-finder/findbrewapp maven)
export PATH=$MAVEN_HOME/bin:$PATH
```

### Alternatives

Should you find yourself not wanting to find where a brew managed app is installed you can do the following via shell script:

```bash
export HOMEBREW_INSTALL_BASE="$(brew --prefix)/Cellar/" 
export MAVEN_VERSION="$(brew info --json=v1 --installed | jq 'map(select(.name == "maven")) | .[0] | .installed | .[0] | .version' | xargs echo)" 
export MAVEN_HOME=$HOMEBREW_INSTALL_BASE"maven/"$MAVEN_VERSION"/libexec"
```

## Authors

* **Allan Ditzel** - *Initial work* - [aditzel](https://github.com/aditzel)

## License

This project is licensed under the ISC License - see the [LICENSE.md](LICENSE.md) file for details.

