# nite-owl

A modular web reconnaissance toolkit written in Python.
Created by **Hex-0verkill**.

```
   ,___,    #   #  #####  #####  #####          ###   #   #  #
   [O.o]    ##  #    #      #    #             #   #  #   #  #
   /)__)    # # #    #      #    ####   #####  #   #  # # #  #
   -"--"-    #  ##    #      #    #             #   #  ## ##  #
            #   #  #####    #    #####          ###   #   #  #####
```

> **Legal notice:** Use nite-owl only against systems you own or have explicit
> written permission to test. Unauthorized scanning may be illegal. The author
> accepts no responsibility for misuse.

## Features

| Module   | Description                                                        |
|----------|--------------------------------------------------------------------|
| `dns`    | A, AAAA, MX, NS, TXT, CNAME and SOA records                        |
| `whois`  | Registrar, creation/expiry dates, name servers                     |
| `http`   | Status, redirects, headers, security-header audit, cookie flags    |
| `tech`   | Technology fingerprinting from headers, cookies and HTML           |
| `tls`    | Certificate details, SANs, expiry, protocol and cipher             |
| `files`  | `robots.txt`, `sitemap.xml`, `security.txt`                        |
| `emails` | Email harvesting from public pages (light same-host crawl)         |
| `subs`   | Subdomains via crt.sh, optional wordlist brute force               |
| `ports`  | TCP connect scan of common ports (active, opt-in only)             |

Results can be saved as JSON, or exported as a formatted PDF report.

## Requirements

- Python 3.8+
- Works on Windows, Linux and macOS

## Installation

```bash
git clone <your-repo-url> nite-owl
cd nite-owl
pip install -r requirements.txt
```

`requests` is required. `dnspython`, `python-whois` and `reportlab` are optional:
the matching features are skipped with a hint if they are missing.

## Usage

```bash
python nite-owl.py <target> [options]
```

### Examples

```bash
# Default scan (everything except the port scan)
python nite-owl.py example.com

# Run specific modules only
python nite-owl.py example.com -m dns http tls

# Email harvesting with a larger crawl, including third-party addresses
python nite-owl.py example.com -m emails --max-pages 60 --all-emails

# Full scan with brute force and port scan, saving JSON and PDF
python nite-owl.py example.com --brute --ports -o report.json --pdf
```

### Options

| Option             | Description                                           |
|--------------------|-------------------------------------------------------|
| `-m`, `--modules`  | Modules to run (default: all except `ports`)          |
| `--brute`          | Enable subdomain wordlist brute force                 |
| `--ports`          | Add the port scan module                              |
| `-t`, `--threads`  | Thread count for brute force / port scan (default 50) |
| `--max-pages`      | Page limit for the email crawl (default 30)           |
| `--all-emails`     | Also list third-party email addresses                 |
| `-o`, `--output`   | Save the JSON report to a file                        |
| `--pdf`            | Save a PDF report automatically, without prompting    |
| `--no-prompt`      | Skip the "print as PDF?" question                     |

After a scan, nite-owl asks whether you want the report printed as a PDF
(unless `--pdf` or `--no-prompt` is given).

## GUI

A Tkinter front end with the same modules and options:

```bash
python nite-owl-gui.py
```

- Enter a target, tick modules and options, confirm authorization, press **RUN SCAN**
- Live colour-coded output, progress bar and a stop button
- **Save JSON** and **Export PDF** buttons (it also offers the PDF when a scan finishes)
- Keep `nite-owl-gui.py` in the same folder as `nite-owl.py`
- On Linux you may need Tkinter: `sudo apt install python3-tk`

## Active vs. passive

- **Passive / low-impact:** `dns`, `whois`, `tls`, `subs` (crt.sh only)
- **Light active (sends requests to the target):** `http`, `tech`, `files`, `emails`
- **Active (more intrusive):** `subs --brute`, `ports`

Choose modules appropriate to your authorization.

## Project layout

```
nite-owl/
├── nite-owl.py        # the command-line tool
├── nite-owl-gui.py    # Tkinter GUI (uses nite-owl.py)
├── requirements.txt   # dependencies
├── LICENSE
└── README.md
```

## Roadmap ideas

- Directory and file discovery
- WAF detection
- HTML report output
- Async scanning
- Shodan / VirusTotal integration

## License

See [LICENSE](LICENSE). Free to use, modify and share as long as credit to
**Hex-0verkill** is kept. For authorized testing only. Provided as is, with no warranty.

## Credits

Created by **Hex-0verkill**.
