# Pkg3

<!--
[![Build Status](https://travis-ci.org/StefanKarpinski/Pkg3.jl.svg?branch=master)](https://travis-ci.org/StefanKarpinski/Pkg3.jl)

[![Coverage Status](https://coveralls.io/repos/StefanKarpinski/Pkg3.jl/badge.svg?branch=master&service=github)](https://coveralls.io/github/StefanKarpinski/Pkg3.jl?branch=master)

[![codecov.io](http://codecov.io/github/StefanKarpinski/Pkg3.jl/coverage.svg?branch=master)](http://codecov.io/github/StefanKarpinski/Pkg3.jl?branch=master)
-->

Next-generation package manager for Julia. Still quite alpha.

Before you can use this, install its dependencies:

```jl
Pkg.add("SHA")
Pkg.add("TerminalMenus")
Pkg.clone("https://github.com/StefanKarpinski/TOML.jl.git")
```

Now load `Pkg3` in Julia 0.6 (0.6 only with precompilation off) to add packages and load them:

```jl
$ path/to/julia.6/julia --compilecache=no

julia> using Pkg3
```

This gives you a `pkg> ` REPL mode, activated (for now) by the `]` key. Currently, this supports three operations: `add`, `rm` and `up`:

```jl
pkg> add JSON
INFO: Resolving package versions
INFO: Cloning [682c06a0-de6a-54ab-a142-c8b1cf79cde6] JSON
INFO: Installing JSON v0.13.0 [9003b4622ec7e553]
INFO: Updating project file /Users/stefan/projects/julia/Project.toml
INFO:  [+] JSON = "682c06a0-de6a-54ab-a142-c8b1cf79cde6"
INFO: Updating manifest file /Users/stefan/projects/julia/Manifest.toml
INFO:  [34da2185] + Compat v0.31.0
INFO:  [682c06a0] + JSON v0.13.0

pkg> add Compat @0.28
INFO: Resolving package versions
INFO: Installing Compat v0.28.0 [0427af7e2c8610c8]
INFO: Updating project file /Users/stefan/projects/julia/Project.toml
INFO:  [+] Compat = "34da2185-b29b-5c13-b0c7-acf172513d20"
INFO: Updating manifest file /Users/stefan/projects/julia/Manifest.toml
INFO:  [34da2185] ↓ Compat v0.31.0 ⇒ v0.28.0

pkg> rm Compat
INFO: Updating project file /Users/stefan/projects/julia/Project.toml
INFO:  [-] Compat = "34da2185-b29b-5c13-b0c7-acf172513d20"
INFO:  [-] JSON = "682c06a0-de6a-54ab-a142-c8b1cf79cde6"
INFO: Updating manifest file /Users/stefan/projects/julia/Manifest.toml
INFO:  [34da2185] - Compat v0.28.0
INFO:  [682c06a0] - JSON v0.13.0

pkg> add JSON @0.10
INFO: Resolving package versions
INFO: Installing JSON v0.10.0 [77699b5cc09b169c]
INFO: Updating project file /Users/stefan/projects/julia/Project.toml
INFO:  [+] JSON = "682c06a0-de6a-54ab-a142-c8b1cf79cde6"
INFO: Updating manifest file /Users/stefan/projects/julia/Manifest.toml
INFO:  [34da2185] + Compat v0.31.0
INFO:  [682c06a0] + JSON v0.10.0

pkg> up
INFO: Resolving package versions
INFO: Updating project file /Users/stefan/projects/julia/Project.toml
INFO:  [no changes]
INFO: Updating manifest file /Users/stefan/projects/julia/Manifest.toml
INFO:  [682c06a0] ↑ JSON v0.10.0 ⇒ v0.13.0
```

Package operations create a `Project.toml` file that record what dependencies your project (or named global environment) has – i.e. what you've explicitly added. It also creates a `Manifest.toml` file that records the exact versions of each of those dependenices and their transitive dependencies – and the graph between them. You can load top-level dependencies via the usual `using JSON` or `import JSON` constructs in the REPL or in Julia scripts.
