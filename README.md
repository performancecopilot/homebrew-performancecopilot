# Homebrew Tap for Performance Co-Pilot

This is a custom Homebrew tap for installing [Performance Co-Pilot (PCP)](https://pcp.io/) on macOS.

## Installation

To install PCP using this tap:

```bash
brew tap performancecopilot/performancecopilot
brew install --cask pcp-perf
```

Or install directly without tapping first:

```bash
brew install --cask performancecopilot/performancecopilot/pcp-perf
```

## About Performance Co-Pilot

Performance Co-Pilot (PCP) is a system performance analysis toolkit that provides:

- Live performance monitoring and logging
- Distributed system monitoring capabilities
- Extensible monitoring framework with agents (PMDAs)
- Flexible data collection and analysis tools
- Integration with visualization tools like Grafana

**Links:**
- **Homepage**: https://pcp.io/
- **Source**: https://github.com/performancecopilot/pcp
- **Documentation**: https://pcp.io/docs/

## What Gets Installed

PCP installs several system services that start automatically:

- **io.pcp.pmcd** - Performance Metrics Collector Daemon
- **io.pcp.pmie** - Performance Metrics Inference Engine
- **io.pcp.pmlogger** - Performance Metrics Logger
- **io.pcp.pmproxy** - Performance Metrics Proxy

**Installation locations:**
- Configuration: `/etc/pcp/`
- Data directory: `/var/lib/pcp/`
- Log files: `/var/log/pcp/`

## Uninstallation

To uninstall PCP:

```bash
brew uninstall --cask pcp-perf
```

This will remove the PCP package and stop all associated services.

## For Maintainers

### Updating for New Releases

When a new version of PCP is released, follow these steps to update the cask:

1. **Download the new DMG** from the [PCP releases page](https://github.com/performancecopilot/pcp/releases):
   ```bash
   curl -LO https://github.com/performancecopilot/pcp/releases/download/X.Y.Z/pcp-X.Y.Z.dmg
   ```

2. **Calculate SHA256 checksum**:
   ```bash
   shasum -a 256 pcp-X.Y.Z.dmg
   ```

3. **Update the cask file** (`Casks/pcp-perf.rb`):
   - Update the `version` field to the new version
   - Update the `sha256` field with the calculated checksum

4. **Test locally** before pushing:
   ```bash
   brew reinstall --cask pcp-perf
   ```

5. **Commit and push changes**:
   ```bash
   git add Casks/pcp-perf.rb
   git commit -m "Update pcp-perf to version X.Y.Z"
   git push
   ```

### Testing Changes Locally

To test local changes before publishing:

```bash
# Tap the local repository
brew tap --force performancecopilot/performancecopilot /Users/psmith/dev/pcp/brew-pcp

# Install from local tap
brew install --cask pcp-perf

# Verify installation
brew list --cask pcp-perf
```

### Cask Audit

To check the cask for issues:

```bash
brew audit --cask --online Casks/pcp-perf.rb
```

## Why a Custom Tap?

The name `pcp` is already taken in Homebrew by an unrelated package. This custom tap uses the name `pcp-perf` to distinguish Performance Co-Pilot while maintaining a clear connection to the project.

## License

This tap repository is maintained independently of the Performance Co-Pilot project.

- **PCP License**: See the [PCP repository](https://github.com/performancecopilot/pcp) for license details
- **This tap**: Provided as-is for the convenience of macOS users

## Contributing

Issues and pull requests are welcome! Please ensure:

- Cask follows [Homebrew Cask style guidelines](https://docs.brew.sh/Cask-Cookbook)
- Changes are tested locally before submitting
- Version updates include updated SHA256 checksums
