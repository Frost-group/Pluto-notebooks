# Pluto notebooks 

These Pluto notebooks are automatically executed using a GitHub action and
deployed to a Github pages website.

https://frost-group.github.io/Pluto-notebooks/

# How to use the template

### 👉 Adding notebooks 

Click on **Add files**, and then **Upload files**. In the next page, upload your `.jl` notebook files.

<img width="400" alt="Schermafbeelding 2021-01-06 om 00 15 06" src="https://user-images.githubusercontent.com/6933510/103710071-67da4f00-4fb4-11eb-9943-b66f26119d36.png">

Your notebooks will run on github every time that you update the files in this repository. To check the progress, click on ["Actions"](./actions), you will find the _workflow_ for the last commit.

<img width="400" alt="Schermafbeelding 2021-01-06 om 00 45 25" src="https://user-images.githubusercontent.com/6933510/103711844-978b5600-4fb8-11eb-8b1b-1e5bdacc1c85.png">

Wait for the Action to finish running your notebook.

Don't worry if it doesn't work immediately! It can take a while for the web page to be ready, even after your settings page says it's done. (Github pages says 20 minutes, but it can take even longer.)

## Update notebook files

To update an existing notebook file, simply repeat Step 2 above! (You can also use **Add files** `>` **Upload files** to _update_ upload a file that already exists on the repository.)


# 💡Tips

### Julia Packages

When your notebook runs on github, no packages are installed. To solve this, you need to **declare a package environment** inside the notebook, using `Pkg`.

For example, instead of:

```julia
using Plots
```

```julia
using PlutoUI
```

You should write:

```julia
begin
    import Pkg
    # activate a clean environment
    Pkg.activate(mktempdir())

    Pkg.add([
        Pkg.PackageSpec(name="Plots"),
        Pkg.PackageSpec(name="PlutoUI"),
        # ... keep adding your packages
    ])

    using Plots
    using PlutoUI
    # ... place all usings and imports into this one cell
end
```

**You can use [this helper tool](https://fonsp.com/article-test-3/pkghelper.html) to generate these commands!**

**Important to note:**

-   Place the Pkg commands and the imports in the same cell.
-   You can use the same setup when running your notebook locally. Julia will re-use existing package installations, so this will only download and install packages the first time.

_In the future, Pluto will automate this process for you!_ 🙈

### Homepage

If you go to the (GitHub Pages) URL of repository, you will see a small index of the notebooks in this repository. You can customize this page, two options are:

-   Create your own `index.html` or `index.md` file, it will be used as the homepage.
-   Rename one of your notebooks to `index.jl`, and it will be the default notebook!
