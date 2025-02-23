# Log Archive Tool

An advanced log archival tool for Linux systems that provides automated log compression, retention management, and integrity verification.

> This project was inspired by the [Log Archive Tool project](https://roadmap.sh/projects/log-archive-tool) from roadmap.sh.

## Project Origin

This tool was developed as part of the roadmap.sh projects collection, which challenged developers to create a CLI tool for archiving logs with features like:
- Command line interface with directory argument support
- Compression of logs into tar.gz format
- Timestamp-based archive naming
- Archive logging capabilities

The tool has been extended with additional features beyond the original requirements to provide a more robust solution.

## Features

- Multiple compression methods support (gzip, bzip2, xz, zstd)
- Configurable retention period
- Checksums verification
- Progress bar visualization
- Detailed logging
- Systemd integration
- Disk space monitoring
- Flexible configuration

## Installation

```bash
git clone https://github.com/zxce3/log-archive.git
cd log-archive
./install
```

The installation script will:
- Create necessary directories
- Install required dependencies
- Set up configuration files
- Create systemd service and timer units

## Configuration

Default configuration file location: `~/.config/log-archive/config`

```bash
# Example configuration
CONFIG[ARCHIVE_DIR]="${HOME}/.local/share/log-archive/archives"
CONFIG[LOG_DIR]="${HOME}/.local/share/log-archive/logs"
CONFIG[COMPRESSION]="zstd"
CONFIG[RETENTION_DAYS]=30
CONFIG[MIN_DISK_SPACE]=500
CONFIG[VERIFY_CHECKSUM]=true
CONFIG[LOG_LEVEL]="INFO"
CONFIG[USE_PROGRESS_BAR]=true
```

## Usage

Basic usage:
```bash
log-archive [OPTIONS] <source-directory>
```

Options:
- `-c, --config <file>` : Use custom config file
- `-m, --compression` : Compression method (gzip|bzip2|xz|zstd)
- `-r, --retention <days>` : Retention period in days
- `-v, --verbose` : Increase verbosity
- `-q, --quiet` : Suppress all output
- `-h, --help` : Show help message

Example:
```bash
log-archive -c custom.conf -m zstd /var/log
```

## Automatic Archival

To enable daily automatic archival:
```bash
systemctl --user enable --now log-archive.timer
```

## Directory Structure

```
~/.local/share/log-archive/
├── archives/     # Archived log files
└── logs/         # Tool operation logs

~/.config/log-archive/
└── config        # Configuration file
```

## Log Format

Archives are named using the format: `logs_archive_YYYYMMDD_HHMMSS.{extension}`

Each archive includes a metadata file (.meta) containing:
- Creation timestamp
- Source directory
- Archive size
- Compression method
- SHA256 checksum

## Requirements

- Linux system
- Bash shell
- Required tools: tar, gzip/bzip2/xz/zstd, pv
- Systemd (for automatic archival)

## License

This project is licensed under the GNU General Public License v2.0 - see the [LICENSE](LICENSE) file for details.
