# ReleaseFileLock

A utility to reveal the evil behind the annoying "Cannot delete file(s) currently being occupied by another process" alert and optionally kill it with one-click. All in user-friendly UX.

## Background and Brief Intro

It's sometimes annoying in Windows OS when we try to delete or move a file/folder before ending up with an alert window stating "`Cannot delete xxx because it's currently occupied by other processes`". Also there lacks official straight-forward way to find out exactly which processes hold the file locked, which could sometimes piss users quite off. Such pain point missed from official feature set should be done right. It's a motivation for developing a tiny, ergonomic utility that reveals the evil behind the scene and provides one-click kill-it feature, all done in user-friendly and aesthetically pleasant UX.

## How to start

[To be Continued]

## Warning and Design Rationale

Although the utility makes it convenient to one-click kill the process holding the file, user should be informed of the potential risk. This could be a dangerous operation since the terminated process might be doing something critical with the file, e.g., flushing file content from memory to disk, or in the mid way of modifying the file non-atomically. Terminating process's access to file carelessly could lead to potential data lost or even disastrous consequence.

> Some programs interact with files in a way that they don't block the access to the file. When other programs change the file content, they refresh in time to reflect the changes. Most of text editor programs fall upon this line. On the other hand, some programs do file I/O in a non-preemptive way. Access to file by other programs are blocked until it decides that it finishes its work and release the lock. Some PDF viewers belong to the former group (e.g. Sumatra), while some others fall within the latter group (e.g. Adobe Acrobat Reader). Both methods have their advantages and disadvantages. It's up to the application developer to make rational and informed design decision on which method makes most sense to their application scenario.

Make sure you understand what the process is doing and the potential consequence of killing the process before issuing killing command.

By default, the kill button issues a xxx signal under the hood. Basically what it does in high level is to courteously "*advise*" the process to terminate itself. It should work well with most processes. But it has no guarantee that every process obeys the rules. When it fails, you could still try the `Force kill` option. `Force kill` option is intentionally hidden at default for safety concern. One can go to the `menu` -> `advanced` -> `Allow force kill` to manually activate the option. User is prompted to make informed decision.

Again, the utility is dedicated for power users and hence favors the [assumption of users being consenting and informed adults](https://mail.python.org/pipermail/tutor/2003-October/025932.html). In a short word, make up your own informed choice when using it.

## License

[WTFPL 2.0](./LICENSE)