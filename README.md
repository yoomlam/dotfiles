
Reminders:
- Copy over settings in `~/.config/chezmoi/chezmoi.toml`
	- configures GPG, so copy over `~/.gnupg` to encrypt files
- Use [pass](https://www.passwordstore.org/) to populate sensitive data in chezmoi.
	- `~/.password-store` should not contain actual passwords
	- `pass` uses GPG, so copy over `~/.gnupg` to access sensitive data for chezmoi templates
- The GPG key password used by both apps is in my typical password manager

passwordstore usage:
- `pass` lists them
- `pass insert <some>/<path>` to add

chezmoi usage ([user guide](https://www.chezmoi.io/user-guide)):
- `chezmoi init $GITHUB_USERNAME`, `chezmoi diff`, and `chezmoi apply -v` [details](https://www.chezmoi.io/quick-start/#using-chezmoi-across-multiple-machines)
- `chezmoi list` shows managed files
- `chezmoi add <file>`
- `chezmoi edit <file>` [how-do-i-edit-my-dotfiles-with-chezmoi](https://www.chezmoi.io/user-guide/frequently-asked-questions/usage/#how-do-i-edit-my-dotfiles-with-chezmoi)
	- If the file was modified outside chezmoi, `chezmoi merge <file>` to merge those changes or `chezmoi re-add <file>` to overwrite with the changes
- Use `git` when ready to commit and push in `chezmoi cd`

chezmoi contents:
- [~/.oh-my-zsh is imported](https://www.chezmoi.io/user-guide/include-files-from-elsewhere/#include-a-subdirectory-from-a-url) and managed in `.chezmoiexternal.toml`, so any modifications would be lost after a `chezmoi apply`
- Only specific plugins are included as specified in `.chezmoiexternal.toml`
