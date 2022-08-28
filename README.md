
# DuplicateFilesFinder
This is a tool to find files that have the same content as determined by a secure hash (ignoring file names, paths, mod dates, etc.).

In each case, we ignore files of length 0 as their hashes would always be a trivial match.

Each of these four variations becomes progressively faster.

## Sequential program
`walk0.go` runs without goroutines and does a sequential file walk.

## Method 1
`walk1.go` uses a fixed pool of worker goroutines and a sequential file walk to send file paths to the workers.

## Method 2
`walk2.go` uses a fixed pool of goroutines, but also starts a new file walk goroutine for each directory in the tree.

## Method 3
`walk3.go` creates a goroutine for each file and directory, but limits the number of goroutines that are allowed to do file system operations (to limit contention).
