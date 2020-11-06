### Python
* Count specific elements in list: `len([x for x in mylist if x==value])`

* Create a 2D matrix: `Matrix = [ [0 for x in range(cols)] for y in range(rows)]`
  Ref. element in row i, col j: `Matrix[i][j]`
  
* Initialize a list with a map function: `map( lambda x: x+1, range(3) ) ==> [1, 2, 3]`

* a list of n zeros: `[0] * n`

* exchange values of two vars: `a, b = b, a`

* [`*, **`]( https://stackoverflow.com/questions/36901/what-does-double-star-asterisk-and-star-asterisk-do-for-parameters)


# git
* Squash (already pushed) 3 commits:
`git rebase -i upstream/onboarding~3 onboarding` (watch the tilde `~`)
(replace `pick` with `fixup`)
`git push -u upstream +onboarding` (watch the `+`)
more: https://stackoverflow.com/questions/5667884/how-to-squash-commits-in-git-after-they-have-been-pushed
