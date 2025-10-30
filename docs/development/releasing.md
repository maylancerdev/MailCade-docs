# Release Process

How to create and publish MailCade releases.

## Release Types

### Stable Releases

Production-ready versions for end users.

**Format**: `v1.0.0`, `v1.1.0`, `v2.0.0`

### Beta Releases

Pre-release versions for testing.

**Format**: `v1.0.0-beta.1`, `v1.1.0-beta.2`

## Automated Releases (Recommended)

GitHub Actions handles building for all platforms.

### Prerequisites

- Push access to repository
- Tag creation permissions

### Release Steps

#### 1. Update Version

Edit `package.json`:

```json
{
  "version": "1.0.0"
}
```

#### 2. Update Changelog

Edit `CHANGELOG.md` (create if missing):

```markdown
# Changelog

## [1.0.0] - 2025-10-30

### Added
- Email search functionality
- Dark mode support

### Fixed
- Email rendering bug
- Memory leak issue

### Changed
- Improved performance
```

#### 3. Commit Changes

```bash
git add package.json CHANGELOG.md
git commit -m "Release v1.0.0"
git push origin main
```

#### 4. Create Tag

```bash
git tag v1.0.0
git push origin v1.0.0
```

#### 5. Wait for Build

GitHub Actions automatically:
1. Builds for macOS, Windows, Linux
2. Creates GitHub release
3. Uploads all artifacts

Monitor: https://github.com/olakunlevpn/MailCade/actions

**Build time**: ~10-15 minutes

#### 6. Edit Release Notes

1. Go to Releases page
2. Click "Edit" on new release
3. Review auto-generated notes
4. Add highlights, breaking changes
5. Save

Done! Release is live.

## Manual Releases

Build locally and publish (single platform only).

### Prerequisites

- GitHub Personal Access Token with `repo` scope
- Set environment variable:

```bash
export GH_TOKEN="your_token_here"
```

### Manual Steps

#### 1-3. Same as Automated

Follow steps 1-3 above.

#### 4. Build and Publish

```bash
# Full build with type checking
npm run build:publish

# Or quick build without type checking
npm run electron:publish
```

**Note**: Only builds for your current platform.

#### 5. Verify Release

Check: https://github.com/olakunlevpn/MailCade/releases

## Version Numbering

Follow [Semantic Versioning](https://semver.org):

**Format**: `MAJOR.MINOR.PATCH`

- **MAJOR**: Breaking changes
- **MINOR**: New features (backward compatible)
- **PATCH**: Bug fixes

**Examples**:
- `1.0.0` → `1.0.1`: Bug fixes
- `1.0.0` → `1.1.0`: New features
- `1.0.0` → `2.0.0`: Breaking changes

## Pre-Release Versions

**Beta releases**:
```bash
# Update version
"version": "1.1.0-beta.1"

# Tag
git tag v1.1.0-beta.1
git push origin v1.1.0-beta.1
```

Mark as pre-release on GitHub.

## Release Checklist

Before creating a release:

### Code Quality
- [ ] All tests pass
- [ ] No lint errors
- [ ] No TypeScript errors
- [ ] Code reviewed

### Documentation
- [ ] CHANGELOG updated
- [ ] README accurate
- [ ] Docs updated for new features
- [ ] Breaking changes documented

### Testing
- [ ] Tested on macOS
- [ ] Tested on Windows (if possible)
- [ ] Tested on Linux (if possible)
- [ ] Migration tested (from previous version)
- [ ] Auto-update tested

### Build
- [ ] Version number updated
- [ ] Build succeeds locally
- [ ] App launches correctly
- [ ] No console errors

## Release Artifacts

Each release includes:

### macOS
- `MailCade-{version}-arm64.dmg` - ARM installer
- `MailCade-{version}-arm64-mac.zip` - ARM archive
- `*.blockmap` - Delta update files

### Windows
- `MailCade-Setup-{version}.exe` - Installer
- `MailCade-{version}.exe` - Portable
- `*.blockmap` - Delta update files

### Linux
- `MailCade-{version}.AppImage` - AppImage
- `mailcade_{version}_amd64.deb` - Debian package
- `mailcade-{version}.x86_64.rpm` - RPM package

## Auto-Update Configuration

Releases automatically work with auto-update:

**Requirements**:
- GitHub releases published
- `.blockmap` files included
- Semantic versioning followed

Users get notified automatically.

## Hotfix Releases

For urgent bug fixes:

```bash
# Create hotfix branch
git checkout -b hotfix/1.0.1

# Fix bug
# ...

# Update version to 1.0.1
# Update CHANGELOG

# Merge and release
git checkout main
git merge hotfix/1.0.1
git tag v1.0.1
git push origin main v1.0.1
```

## Release Schedule

**Stable releases**: As needed  
**Minor updates**: Every 1-2 months  
**Patch releases**: As needed for bugs  
**Beta releases**: Weekly during development

## Deprecation Policy

When removing features:

1. **Announce** in release notes
2. **Deprecate** in version N
3. **Remove** in version N+1 (major)

Give users at least one major version to migrate.

## Breaking Changes

Document clearly:

```markdown
## [2.0.0] - Breaking Changes

### BREAKING
- Removed legacy API
- Changed settings format

### Migration Guide
- Old settings automatically migrated
- Update app integrations: [link to guide]
```

## Security Releases

For security fixes:

1. Fix in private
2. Release immediately
3. Announce after release
4. Credit reporter (if desired)

## Rollback Plan

If release has critical bugs:

1. Yank release from GitHub (hide it)
2. Fix bug quickly
3. Release patch version
4. Announce rollback

## Post-Release

After each release:

1. **Announce** on GitHub Discussions
2. **Monitor** for issues (first 24-48 hours)
3. **Respond** to bug reports quickly
4. **Plan** next release

## Common Issues

### Build Fails

- Check TypeScript errors
- Verify all dependencies installed
- Clean build: `rm -rf dist dist-electron release`

### Tag Already Exists

```bash
# Delete local tag
git tag -d v1.0.0

# Delete remote tag
git push origin :refs/tags/v1.0.0

# Create new tag
git tag v1.0.0
git push origin v1.0.0
```

### GitHub Actions Fails

1. Check Actions tab for errors
2. Fix issues
3. Force push or create new tag

## Release Metrics

Track these metrics:

- Downloads per release
- Update adoption rate
- Crash reports
- User feedback
- Performance metrics

## What's Next?

- [Building](building.md) - Build from source
- [Contributing](contributing.md) - Contribute code
