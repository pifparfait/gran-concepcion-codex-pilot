# Issue #7 audit receipt rehearsal

Base pilot revision: 5b6ace977167efbfd8c414384ae9766f74ff380a.
Scientific reference: 162eacecbd93f60b700288ec9b7ff3e26858636e.
Order comment: 6890237836. Its observed UTF-8 body SHA-256 is
770c17a0eadca29efe3bbf055b2aa8dee5d370c7e066f7ab60d1872387c3cf7d.
The observed digest records what was read and grants no execution authority.

Overlay the two Python files and the workflow at their relative paths in an
isolated pilot checkout. The proposed workflow is manually dispatched and runs
only the offline unit tests. It does not use the existing polling workflow or
the Codex action. It requires only repository contents read permission.

Run from the overlay root:

    python3 -IB -m unittest discover -s . -p test_issue7_audit.py -v

The tests rehearse a fresh runner reconstructing the same fixed receipt and
recovering a simulated posted receipt from an authenticated listing. The SQLite
database is local. A published receipt would make observation discoverable
between runners, but does not implement an atomic execution claim.

For a later live receipt trial, review the pinned comment digest and publisher
identity, use a complete authenticated paginated listing, serialize publishers
per order, and reconcile any uncertain POST before retrying. Test actual
publication and readback as a separate trial. For live audit execution, use a
separate authorized single-use permit and durable atomic claim before dispatch.
A missing receipt or an Issue comment must never act as an execution permit.
