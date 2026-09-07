# Employee backend · Starter

A minimal Express server for an employee-management exercise. The current implementation exposes a root route returning a test response; employee CRUD routes are not present.

**Collection:** Starters and experiments · [Project directory](https://github.com/Rspinelli93/Rspinelli93/blob/main/PROJECTS.md)

**Related repository:** [employee-front](https://github.com/Rspinelli93/employee-front)

## Stack

`express`.

## Run locally

Install Node.js and npm, then run:

```bash
git clone https://github.com/Rspinelli93/employee-back.git
cd employee-back
npm install
npm start
```

The start script uses Node’s `--watch` option; use a Node version that supports it.

## Available commands

| Command | Script in package.json |
| --- | --- |
| `npm run start` | `node --watch index.js` |

The `test` script is a placeholder; an automated test suite is not configured through that command.

## Implementation notes

Open `http://localhost:3000/` for the existing JSON test response. There is no database or employee model in this snapshot.

## Repository guide

- [`index.js`](index.js)
- [`package.json`](package.json)

---

[Back to my GitHub profile](https://github.com/Rspinelli93)
