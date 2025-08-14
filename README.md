# About This Fork

**This is a fork of the original repo [ts-error-translator.nvim](https://github.com/dmmulroy/ts-error-translator.nvim).**

I forked this project to address some issues I encountered and to change a few things that I found bothersome.

**Main changes in this fork:**
1. Fixed translations not working for functions that do not receive the correct number of arguments.
2. Changed the notification message to display `Translation:` instead of `Typescript translation(s):`. More inline with original vs code extension.
3. Removed link references to documentation.

---

# ts-error-translator.nvim

![image](https://github.com/dmmulroy/ts-error-translator.nvim/assets/2755722/5fcd1f42-d941-491b-a89b-33ab3c2ed29b)

A Neovim port of [Matt Pocock's ts-error-translator for VSCode](https://github.com/mattpocock/ts-error-translator) for turning messy and confusing TypeScript errors into plain English.

## Installation

To install the plugin, use your preferred Neovim plugin manager.

### lazy.nvim

To install the plugin using lazy.nvim, add the following to your plugin configuration:

```lua
{ 'nemanjamalesija/ts-error-translator.nvim' }
```

### Packer

To install the plugin using packer.nvim, add the following to your plugin configuration:

```lua
use('nemanjamalesija/ts-error-translator.nvim',)
```

### Vim-Plug

To install the plugin using vim-plug, add the following to your plugin configuration:

```vim
Plug 'nemanjamalesija/ts-error-translator.nvim'
```

Then run `:PlugInstall` to install the plugin.

## Setup

To set up the plugin, add the following line to where you manage your plugins:

```lua
require("ts-error-translator").setup()
```

## Configuration

By default, `ts-error-translator.nvim` will attach itself to your `tsserver`
lsp and automatically start translating errors for you. The following is the
default configuration for the plugin:

```lua
{
  auto_override_publish_diagnostics = true,
}
```

If you want to override `tsserver`'s `textDocument/publishDiagnostics` handler
`manually, ts-error-translator.nvim` exports a function,
`require('ts-error-translator').translate_diagnostics`, that you can
then use to override your lsp handlers. Here is example usage:

```lua
vim.lsp.handlers["textDocument/publishDiagnostics"] = function(err, result, ctx)
  require("ts-error-translator").translate_diagnostics(err, result, ctx)
  vim.lsp.diagnostic.on_publish_diagnostics(err, result, ctx)
end
```

## Related

If you like this plugin and find it useful, you might also like my plugin, [tsc.nvim](https://github.com/dmmulroy/tsc.nvim), a Neovim plugin for seamless, asynchronous project-wide TypeScript type-checking using the TypeScript compiler (tsc)

## Contributing

Feel free to open issues or submit pull requests if you encounter any bugs or have suggestions for improvements. Your contributions are welcome!

## License

This plugin is released under the MIT License. See the [LICENSE](LICENSE) file for details.

## Acknowledgements

A special thanks to [Matt Pocock](https://github.com/mattpocock) for creating the `ts-error-translator`, providing the foundation for this project.
