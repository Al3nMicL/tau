# Session and project archiving

The `/resume` picker can archive its highlighted session or the highlighted
project with **Delete**. Archiving removes session metadata from the resume
indexes. It never removes JSONL transcripts, project directories, or other user
files. Archived sessions and projects therefore disappear from the picker while
their on-disk conversations remain untouched.

`SessionManager.archive_session()` and `SessionManager.archive_project()` own the
persisted behavior. The Textual picker calls those methods off the UI thread and
only removes the archived row after persistence succeeds. Archiving one session
leaves its project's other sessions visible; archiving the project removes all of
its rows from the picker.

Tests cover index removal, repeated/idempotent archive calls, preservation of
transcripts and directories, and both picker columns.
