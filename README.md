
Reminders:
- Copy over and modify settings in `~/.config/chezmoi/chezmoi.toml`
	- configures GPG, so copy over `~/.gnupg` to encrypt files
- Use [pass](https://www.passwordstore.org/) to populate sensitive data in chezmoi templates
	- `pass` uses GPG, so copy over `~/.gnupg`

Sensitive storage options from least to most secure:
1. Store as clear text in `~/.config/chezmoi/chezmoi.toml` as `[data]` per machine (not in git) and use chezmoi template.
2. `chezmoi add --encrypt <file>` uses GPG to encrypt the file based on config in GPG config in `chezmoi.toml` and store in git repo.
3. Store in `~/.password-store` (not in git) using GPG key and use chezmoi template.
	- `~/.password-store` should not contain actual passwords
	- `~/.password-store/.gpg-id` specifies the GPG key to use
4. Store in typical password manager
	- The password for the GPG key (used by both `chezmoi` and `pass`) is in my typical password manager

passwordstore usage:
- `pass` lists them
- `pass insert <some>/<path>` to add
- test chezmoi's access: `chezmoi execute-template '{{ pass "<some>/<path>" }}'`
- test the template file: `chezmoi cat <dotfile>`

chezmoi usage ([user guide](https://www.chezmoi.io/user-guide)):
- `chezmoi init $GITHUB_USERNAME`, `chezmoi diff`, and `chezmoi apply -v` [details](https://www.chezmoi.io/quick-start/#using-chezmoi-across-multiple-machines)
	- file naming reflects [state attributes](https://www.chezmoi.io/reference/source-state-attributes/)
- `chezmoi list` shows managed files
- `chezmoi add <file>`
- `chezmoi edit <file>` [how-do-i-edit-my-dotfiles-with-chezmoi](https://www.chezmoi.io/user-guide/frequently-asked-questions/usage/#how-do-i-edit-my-dotfiles-with-chezmoi)
	- If the file was modified outside chezmoi, `chezmoi merge <file>` to merge those changes or `chezmoi re-add <file>` to overwrite with the changes
- Use `git` when ready to commit and push in `chezmoi cd`

chezmoi contents:
- [~/.oh-my-zsh is imported](https://www.chezmoi.io/user-guide/include-files-from-elsewhere/#include-a-subdirectory-from-a-url) and managed in `.chezmoiexternal.toml`, so any modifications would be lost after a `chezmoi apply`
- Only specific plugins are included as specified in `.chezmoiexternal.toml`
