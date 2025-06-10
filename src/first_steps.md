# new repository

## command table

| command                   | action                                    |
| :------------------------ | :---------------------------------------- |
| jj git init               | initialize the repository                 |
| jj st                     | show the repository status                |
| jj desc                   | create (update) the change description    |
| jj bookmark create        | create new bookmark (like a branch)       |
| jj git remote add origin  | add a remote server                       |
| jj git push --allow-new   | push to the remote for the first time     |

## discussion

every time i start a new Rust project, the first thing i do after running
`cargo new` is to create its remote repo. so i thought that a good "hello
world" for *jj* would be to achieve the same as that initial instructions
provided by github when creating a new repository, i.e.:

```sh
echo "# new-repo" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:lpnh/new-repo.git
git push -u origin main
```

but i think we could replace the readme file with a Rust project

## cargo new

so, we can get our "hello world" from Rust by simply running `cargo new
<project-name>`, and right of the bet we will discover that we will have to
update our workflow

the reason is that by default cargo already provides a git repository for us

let me share what my terminal looks like when running `ls --all` inside the
project directory

```sh
my-rust-project on  master [?] via 🦀 v1.87.0
♥  ls --all
./  ../  Cargo.toml  .git/  .gitignore  src/
```

so we can confirm that a git repo was generated for us noticing the presence of
the `.git/` directory

before we discuss how to avoid this, i would like to bring attention to
something else we can also notice on my prompt:

```sh
on  master [?] via 🦀 v1.87.0
```

the `starship`'s `git_branch` module shows us we are currently at the *master*
branch with *untracked* files (represented by the `?` mark). we can verify it
by running `git status`, which provides the following output:

```sh
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	.gitignore
	Cargo.toml
	src/

nothing added to commit but untracked files present (use "git add" to track)
```

ok. let's take a moment here to recapitulate: with a simple `cargo new` we got
a git repository with a branch named *master* and no commits. all our project
files are not yet tracked by git. this is why it suggests us to run the `git
add` command so these files will be tracked and included in a future commit
