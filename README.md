# Tailwind v4 with Dioxus 0.63 Desktop

These are the steps I arrived at to get a Tailwind CSS v4 project up and running with Dioxus 0.63 Desktop.

## Install Dioxus

Just straight from the [getting started](https://dioxuslabs.com/learn/0.6/getting_started/#) instructions:

    cargo install cargo-binstall
    cargo binstall dioxus-cli

## Install Tailwind CSS

Example from [documentation](https://tailwindcss.com/docs/installation) for macOS arm64:

    curl -sLO https://github.com/tailwindlabs/tailwindcss/releases/latest/download/tailwindcss-macos-arm64
    chmod +x tailwindcss-macos-arm64
    mv tailwindcss-macos-arm64 tailwindcss

What I actually did on my x86 Ubuntu machine:

    curl -sLO https://github.com/tailwindlabs/tailwindcss/releases/download/v4.0.9/tailwindcss-linux-arm64
    mv tailwindcss-linux-arm64 ~/bin/tailwindcss
    chmod +x ~/bin/tailwindcss

## Create the project

1. `dx new tailwind-dioxus-desktop`
  1. Jumpstart
  1. Fullstack false
  1. Router true
  1. Tailwindcss true
  1. Platform desktop
1. `cd tailwind-dioxus-desktop`
1. Replace [input.css](./input.css) (click to view file)
1. In [tailwind.config.js](./tailwind.config.js), replace `module.exports =` with `export default` (optional)
1. In a new console or IDE: `tailwindcss -i input.css -o assets/tailwind.css -w`, let that stay running
1. Observe that [assets/tailwind.css](./assets/tailwind.css) now has some CSS content in it, which it didn't before
1. In another console: `dx serve`
1. Profit (optional)

## Daisy bonus round

1. Update [src/main.rs](./src/main.rs) to add a new line 36 with

    document::Link { href: "https://cdn.jsdelivr.net/npm/daisyui@5", rel: "stylesheet", type: "text/css" }

## Zed bonus round

1. ^-shift-P, `zed: open project tasks`
1. Add the tasks:
    // ...
      {
        "label": "Dioxus Serve",
        "command": "dx serve --platform desktop",
        "use_new_terminal": true,
        "allow_concurrent_runs": false,
        "reveal": "no_focus",
        "hide": "on_success"
      },
      {
        "label": "Tailwind Watch",
        "command": "tailwindcss -i input.css -o assets/tailwind.css -w",
        "use_new_terminal": true,
        "allow_concurrent_runs": false,
        "reveal": "no_focus",
        "hide": "on_success"
      },
    // ...
1. Save and close the tasks file
1. Alt-shift-T, `Tailwind Watch`
1. Alt-shift-T, `Dioxus Serve`
