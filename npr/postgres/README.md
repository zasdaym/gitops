# Postgres credentials

The Password generator supplies a random 32-character password to PushSecret.
PushSecret creates `/postgres/POSTGRES_PASSWORD` in Infisical only if it is
missing. It preserves existing values and leaves the remote secret in place
when PushSecret is deleted.

ExternalSecret reads the password and all other values under `/postgres` into
the `postgres` Kubernetes Secret. It requires `POSTGRES_PASSWORD` to exist
before syncing. Postgres consumes only this provider-backed Secret.

The `/postgres` folder must exist in the configured Infisical environment.
The store's machine identity needs permission to read the project and secrets
and create secrets in that folder.

For an existing database, keep its current password in Infisical before syncing.
Generating a password does not change the password in an initialized database.

ExternalSecret owns the Kubernetes Secret, so deleting ExternalSecret also
deletes that Secret. The Infisical value remains available for recovery.
