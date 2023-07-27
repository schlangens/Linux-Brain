## SSH

### Generate SSH Key

1.  Open Terminal.
2.  Paste the text below, substituting in your GitHub email address.

    ```shell
    $ ssh-keygen -t ed25519 -C "your_email@example.com"
    ```

    **Note:** If you are using a legacy system that doesn't support the Ed25519 algorithm, use:

    ```shell
    $ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
    ```

- When you're prompted to "Enter a file in which to save the key," press Enter. This accepts the default file location.

  ```shell
  > Enter a file in which to save the key (/Users/you/.ssh/id_algorithm): [Press enter]
  ```

- At the prompt, type a secure passphrase. For more information, see ["Working with SSH key passphrases](https://docs.github.com/en/articles/working-with-ssh-key-passphrases).

### Adding or changing a passphrase

You can change the passphrase for an existing private key without regenerating the keypair by typing the following command:

```shell
$ ssh-keygen -p -f ~/.ssh/id_ed25519
> Enter old passphrase: [Type old passphrase]
> Key has comment 'your_email@example.com'
> Enter new passphrase (empty for no passphrase): [Type new passphrase]
> Enter same passphrase again: [Repeat the new passphrase]
> Your identification has been saved with the new passphrase.
```

If your key already has a passphrase, you will be prompted to enter it before you can change to a new passphrase.

On Mac OS X Leopard through OS X El Capitan, these default private key files are handled automatically:

- _.ssh/id_rsa_
- _.ssh/identity_

The first time you use your key, you will be prompted to enter your passphrase. If you choose to save the passphrase with your keychain, you won't have to enter it again.

Otherwise, you can store your passphrase in the keychain when you add your key to the ssh-agent. For more information, see "[Adding your SSH key to the ssh-agent](https://docs.github.com/en/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent#adding-your-ssh-key-to-the-ssh-agent)."

### How to check your current keys

- Open Terminal.
- Enter `ls -al ~/.ssh` to see if existing SSH keys are present.

  ```shell
  $ ls -al ~/.ssh
  # Lists the files in your .ssh directory, if they exist
  ```

- Check the directory listing to see if you already have a public SSH key. By default, the filenames of supported public keys for GitHub are one of the following.

  - _id_rsa.pub_
  - _id_ecdsa.pub_
  - _id_ed25519.pub_

- **Tip**: If you receive an error that _~/.ssh_ doesn't exist, you do not have an existing SSH key pair in the default location. You can create a new SSH key pair in the next step.
- Either generate a new SSH key or upload an existing key.

  - If you don't have a supported public and private key pair, or don't wish to use any that are available, generate a new SSH key.
  - If you see an existing public and private key pair listed (for example, _id_rsa.pub_ and _id_rsa_) that you would like to use to connect to GitHub, you can add the key to the ssh-agent.

    For more information about generation of a new SSH key or addition of an existing key to the ssh-agent, see "[Generating a new SSH key and adding it to the ssh-agent](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)."

### Adding a new SSH key to your clipboard

- Copy the SSH public key to your clipboard.

  If your SSH public key file has a different name than the example code, modify the filename to match your current setup. When copying your key, don't add any newlines or whitespace.

  ```shell
  $ pbcopy < ~/.ssh/id_ed25519.pub
  # Copies the contents of the id_ed25519.pub file to your clipboard
  ```

  **Tip:** If `pbcopy` isn't working, you can locate the hidden `.ssh` folder, open the file in your favorite text editor, and copy it to your clipboard.

### Adding your SSH key to the ssh-agent

Before adding a new SSH key to the ssh-agent to manage your keys, you should have checked for existing SSH keys and generated a new SSH key. When adding your SSH key to the agent, use the default macOS `ssh-add` command, and not an application installed by [macports](https://www.macports.org/), [homebrew](http://brew.sh/), or some other external source.

- Start the ssh-agent in the background.

  ```shell
  $ eval "$(ssh-agent -s)"
  > Agent pid 59566
  ```

  Depending on your environment, you may need to use a different command. For example, you may need to use root access by running `sudo -s -H` before starting the ssh-agent, or you may need to use `exec ssh-agent bash` or `exec ssh-agent zsh` to run the ssh-agent.

If you're using macOS Sierra 10.12.2 or later, you will need to modify your `~/.ssh/config` file to automatically load keys into the ssh-agent and store passphrases in your keychain.

- First, check to see if your `~/.ssh/config` file exists in the default location.

  ```shell
  $ open ~/.ssh/config
  > The file /Users/you/.ssh/config does not exist.
  ```

- If the file doesn't exist, create the file.

  ```shell
  $ touch ~/.ssh/config
  ```

- Open your `~/.ssh/config` file, then modify the file to contain the following lines. If your SSH key file has a different name or path than the example code, modify the filename or path to match your current setup.

```
Host *
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/id_ed25519
```

**Note:** If you chose not to add a passphrase to your key, you should omit the `UseKeychain` line.

**Note:** If you see an error like this

```
/Users/USER/.ssh/config: line 16: Bad configuration option: usekeychain
```

add an additional config line to your `Host *` section:

```
Host *
  IgnoreUnknown UseKeychain
```

Add your SSH private key to the ssh-agent and store your passphrase in the keychain. If you created your key with a different name, or if you are adding an existing key that has a different name, replace _id_ed25519_ in the command with the name of your private key file.

```shell
$ ssh-add -K ~/.ssh/id_ed25519
```

**Note:** The `-K` option is Apple's standard version of `ssh-add`, which stores the passphrase in your keychain for you when you add an SSH key to the ssh-agent. If you chose not to add a passphrase to your key, run the command without the `-K` option.

If you don't have Apple's standard version installed, you may receive an error. For more information on resolving this error, see "[Error: ssh-add: illegal option -- K](https://docs.github.com/en/articles/error-ssh-add-illegal-option-k)."

In MacOS Monterey (12.0), the `-K` and `-A` flags are deprecated and have been replaced by the `--apple-use-keychain` and `--apple-load-keychain` flags, respectively.

Add the SSH key to your account on GitHub. For more information, see "[Adding a new SSH key to your GitHub account](https://docs.github.com/en/github/authenticating-to-github/adding-a-new-ssh-key-to-your-github-account)."
