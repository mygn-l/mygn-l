## Workflow

### Initial phase

- Gather all the information on the project from Linear and Slack.
- Read the relevant repos in depth, not just skimming.
- Plan the project.
- Search for known approaches first, and judge whether one fits or your own design or redesign is needed.
- For each problem, find the appropriate model, such as the data structure (see [data-structures.md](data-structures.md) for examples).

### Building phase

- Before writing any code, gather the information and measurements needed to write it; if something can't be known yet, move on and come back to it.
- Never wait blind on a background task; check it on a repeating timer with a period that fits it.

### Review phase

- Go back over every open point that was left or forgotten.
- Clean up the code, such as removing what's unused.
- Check that every change stays within the project's scope; flag anything found that is someone else's responsibility.
- Run all tests.
- Edit the Linear project to match the work, keeping it short: its issues, their comments, and their attached files and PRs (see [linear.md](linear.md)).

### Deploy phase

- Before committing, leave out anything that doesn't belong in the commit.
- Before pushing, run the CI checks locally, comment density included, so no time is wasted on a failed CI run.
- Open a new PR from a new branch, targeting the staging or development branch where there is one.
- Never post anything that notifies many people at once, such as a project update in Linear.

## General

### Functions

- A function has a domain; every possible input in it is considered when writing the function.
- A function has a range: the values it is allowed to return.
- A function's side effects, both reads and writes, are considered.

### Constants

- Constants, settings and defaults are defined once, in a named place (a file constant, the database, config, an env var or a flag), never inline.

### Errors

- Where appropriate, a failure throws an error instead of returning a status.

### Naming

- Name everything with the established terms; never invent your own.
- Use snake_case.

### Tests

- Only regression tests.

## Web development

### API

- CRUD at its core; other endpoints only for operations that aren't CRUD.
- Every endpoint is permission gated.
- Inputs are validated for type, then cleaned; the clean value must be fully safe.
- Cleaning never merges inputs that mean different things; in particular, absent, null, empty and zero stay distinct.
- Every request gets the appropriate response with the correct status code, including those that stop before the clean value.
- Routes only route. Validation, cleaning and business logic come from imported code.
- Each endpoint passes the cleaned value to services.

### Services

- Services handle every case the cleaned value can hold.
- Services return the appropriate result, such as an outcome status or the value read.

### Data

- Data is read and written only from the service layer, even when the service is a thin wrapper.
- Where applicable, stored data keeps absent, null, empty and zero distinct.
- Queries always pass values as query parameters, never built into the query string.
- State lives in a shared session store (such as Redis) or the database, never in a container's memory.

### UI

- Critical actions ask for confirmation.
- Long lists are paginated, not loaded whole.
