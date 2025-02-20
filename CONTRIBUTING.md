## Semantic Pull Requests

To generate release and generate changelog, Pull Requests or Commits must have semantic and must follow conventional specs below:
```
PR Name: <type>:<description>
[optional body]
[optional footer(s)]
[required]Label - one of the following:
```
- `feat:` New feature (non-breaking change which adds functionality)
- `fix:` Bug fix (non-breaking change which fixes an issue)
- `docs:` Documentation
- `refactor:`  Code refactor
- `chore:` Changes to the build process or auxiliary tools and libraries such as documentation generation

1. If the label is “BREAKING CHANGE” then MAJOR version is incremented.
2. If the label is "feat" then MINOR version is incremented.
3. If the label is "fix" then the PATCH version is incremented.
4. If the label is doc/refactor/chore, then nothing is increment and no release is made.

Example commits:
```
feat: added 'ref' parameter to choose branch for commits
```
```
fix: correcting 'ref' parameter
```
```
feat: adding new parameter 
BREAKING CHANGE: adding some BREAKING CHANGE functionalities
```