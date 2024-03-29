# install Ruby 

using ruby installation manager
- https://github.com/rbenv/rbenv
- https://github.com/rvm/rvm
- https://hixonrails.com/ruby-on-rails-tutorials/ruby-environment-management/

## via rbenv

https://www.digitalocean.com/community/tutorials/how-to-install-ruby-on-rails-with-rbenv-on-ubuntu-20-04
https://www.digitalocean.com/community/tutorials/how-to-install-ruby-on-rails-with-rbenv-on-macos

1. show list of ruby versions

- check only stable list `rbenv install -l`
- check all list available `rbenv install -L`

2. after getting list and decided the version that you wanna install, run `rbenv install 3.1.1` or `rbenv install 2.7.5` or any version you like
3. set global by running `rbenv global 3.1.1`
4. check all version installed in your pc by running `rbenv versions`



## via RVM

http://rvm.io/rvm/install

1. add gpg key 

```
gpg --keyserver hkp://pool.sks-keyservers.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB
```

2. install rvm

```
curl -sSL https://get.rvm.io | bash -s stable
```

3. install Ruby version

```
rvm install 2.7.5 
```

4. check the list `rvm list`
5. let's make this more interesting by install another version `rvm insall 3.0.0`
6. again check the list `rvm list`
7. see other commands available `rvm help`
8. uninstall rvm `rvm implode`

# install rails

source: https://www.aloucaslabs.com/miniposts/using-a-specific-rails-version-when-you-generate-a-new-rails-app-with-rails-new-command

1. install gem dan cari versi rail yang kamu ingin install `gem search '^rails$' --all`
2. kalau udah ketemu install dengan jalankan `gem install rails -v 6.1.4.1`
3. tampilkan daftar rail yang udah diinstal `gem list rails --local`
4. atau semua gem yang terinstall `gem list --local`
5. install specific rail version `rails _6.1.4.1_ new appname`
6. go to folder app and run sync `rails s` then open http://localhost:3000/ on your browser
7. check local rail version run `rails -v` in app folder but for global `cd ..` then run `rails -v`

# Ruby-GoLang Comparison

| ruby | golang |
|--------|-------|
| _Gemfile.lock_ | _go.sum_ |
| _Gemfile_ | _go.mod_ |
| `bundle i` | `go mod tidy` |
| `bundle init` or `rails new app_name` | `go mod init project_name` |

# Class and Object
An object is an instance of the class
- [stackoverflow: nested classes/module](https://stackoverflow.com/questions/6195661/when-to-use-nested-classes-and-classes-nested-in-modules)

# VS-Code configuration

in `settings.json` of vscode (ctrl+shift+p, open workspace setting), put this configuration

```json
{
    "[ruby]": {
        "editor.defaultFormatter": "rubocop.vscode-rubocop"
      },
      "editor.formatOnSave": true,
      "rubocop.autocorrect": true,
      // if true, will complain the missing frozen string literal comment but not correct it
      // if false, will complain and correct it
      // true by default
      "rubocop.safeAutocorrect": true,
      // if true, only lint and correct the unused variable
      // false by default
      "rubocop.lintMode": true,
      // if true, only correct layout
      // if false, correct the lint also including the missing frozen string literal
      // false by default
      "rubocop.layoutMode": true,
      // true by default
      "rubocop.yjitEnabled": true,
}
```

update: 28-03-2024

```json
{
    "[ruby]": {
        // "editor.defaultFormatter": "Shopify.ruby-lsp", // Use the Ruby LSP as the default formatter
        // "editor.defaultFormatter": "rubocop.vscode-rubocop",
        "editor.defaultFormatter": "castwide.solargraph",

        "editor.formatOnSave": true, // Format files automatically when saving
        "editor.tabSize": 2, // Use 2 spaces for indentation
        "editor.insertSpaces": true, // Use spaces and not tabs for indentantion
        "editor.semanticHighlighting.enabled": true, // Enable semantic highlighting
        "editor.formatOnType": true // Enable formatting while typing
      },
      "rubyLsp.formatter": "auto",
      "rubyLsp.rubyVersionManager": "rbenv",

      "rubocop.autocorrect": true,
      "rubocop.safeAutocorrect": true,
      "rubocop.lintMode": true,
      "rubocop.layoutMode": true,
      "rubocop.yjitEnabled": true,

      "solargraph.autoformat": true,
      "solargraph.formatting": true
}
```

references:
- https://rubocop.org/
- https://sorbet.org/
- https://solargraph.org/
- https://shopify.github.io/ruby-lsp/index.html

# Sample Ruby Project

## Gem

- https://github.com/sferik/x-ruby
- https://github.com/sferik/twitter-ruby

# Notes

- https://guides.rubygems.org/make-your-own-gem/



