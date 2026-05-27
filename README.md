# Demo website for the VnG Blue Hugo theme

See more about VnG Blue Hugo theme [here](https://github.com/ismd/hugo-theme-vng-blue).

Deployed demo website is [here](https://ismd.github.io/demo-hugo-theme-vng-blue/).

## Local theme development

The `go.mod` file contains a `replace` directive that points the theme module to a local checkout:

```
replace github.com/ismd/hugo-theme-vng-blue => /home/ismd/coding/hugo-theme-vng-blue
```

This lets Hugo pick up theme changes immediately without publishing a new version. Before committing or deploying, remove (or comment out) the `replace` line so the build uses the published module version listed in `require`.
