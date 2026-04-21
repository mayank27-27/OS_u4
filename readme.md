# PES-VCS — Theory Answers (Phase 5 & 6)

## Phase 5 — Version Control Concepts

### 1. Checkout Process
Checkout is the operation of switching the working directory to match a specific commit or branch.

Steps involved:
- Update HEAD to point to the target commit or branch
- Read the tree object associated with that commit
- Restore files in the working directory based on the tree
- Update index to reflect the checked-out state

---

### 2. Dirty Working Directory
A working directory is considered "dirty" when it contains changes that are not committed.

Detection methods:
- Compare file metadata (mtime, size) with index
- Recompute hash and compare with stored object hash
- Identify modified, deleted, or newly created files

Why it matters:
- Prevents overwriting uncommitted changes
- Ensures data safety before checkout or commit

---

### 3. Detached HEAD
A detached HEAD occurs when HEAD points directly to a commit instead of a branch.

Characteristics:
- New commits are not associated with any branch
- History can be lost if not referenced later

Example:
- Checking out a specific commit hash instead of a branch

---

## Phase 6 — Garbage Collection

### 1. Reachability Analysis
Garbage collection determines which objects are still in use.

Process:
- Start from all references (HEAD, branches)
- Traverse commits → trees → blobs
- Mark all reachable objects

---

### 2. Cleanup of Unreachable Objects
Objects not reachable from any reference are considered garbage.

Steps:
- Identify unreachable objects
- Delete them from `.pes/objects`

Benefit:
- Saves storage space
- Keeps repository clean

---

### 3. Race Conditions
Race conditions occur when multiple operations happen simultaneously, causing inconsistencies.

Example:
- Garbage collection runs while a commit is being created

Problems:
- Valid objects may be deleted accidentally

Solutions:
- Use locking mechanisms
- Delay garbage collection during commits
- Ensure atomic operations
