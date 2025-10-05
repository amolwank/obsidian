What is Canary Deployment?
- A progressive delivery strategy where a new version of an application is released gradually to a small subset of users before rolling out to everyone.
- Unlike Blue-Green (all traffic switches at once), Canary allows incremental testing in production.
- If the new version is stable, you slowly increase traffic until 100%, If it fails, rollback is quick.