#  Project Honeypy

A **honeypot** is a security tool that simulates a vulnerable environment to attract potential attackers. It allows us to safely observe and analyze unauthorized access attempts, helping improve security defenses by understanding attacker behavior.

This project includes SSH and HTTP honeypot applications to simulate a vulnerable server environment, capturing unauthorized login attempts and logging user actions. The main `honeypy.py` file acts as an entry point, allowing users to start either honeypot type based on specified arguments.

This project was created by following [Grant Collins tutorial](https://youtu.be/gDjDxS55890?si=4K_QVw02pjt2_-Uf) and with additional guidance from ChatGPT.

## Files

- **`ssh_honeypot.py`**: Implements an SSH-based honeypot.
  - **Libraries Used**: `logging`, `socket`, `paramiko`, `threading`, and `time`.
  - **Functionality**:
    - Listens for SSH connections and logs login attempts, including username and password combinations.
    - Emulates a shell environment with commands like `pwd`, `whoami`, and `ls`.
    - Logs all commands entered by the client.
  - **Logging**:
    - `audits.log`: Logs all SSH connection attempts with credentials.
    - `cmd_audits.log`: Logs commands executed by connected clients.

- **`web_honeypot.py`**: Implements a web-based honeypot using Flask.
  - **Libraries Used**: `logging`, `Flask`.
  - **Functionality**:
    - Hosts a web page that mimics a login page.
    - Logs all login attempts along with IP addresses and credentials.
    - Displays success or failure messages based on predefined credentials.
  - **Logging**:
    - `http_audits.log`: Logs IP addresses, usernames, and passwords used in login attempts.

- **`honeypy.py`**: The main script to initiate the SSH or HTTP honeypot.
  - **Libraries Used**: `argparse`, imports `ssh_honeypot` and `web_honeypot`.
  - **Arguments**:
    - `-a` / `--address` (required): IP address to bind the honeypot.
    - `-p` / `--port` (required): Port number for the honeypot.
    - `-u` / `--username` (optional): Username for authentication.
    - `-pw` / `--password` (optional): Password for authentication.
    - `-s` / `--ssh` (optional): Enable SSH honeypot.
    - `-w` / `--http` (optional): Enable HTTP honeypot.

## Usage

To start a honeypot, run `honeypy.py` with the required options.

### Example Commands

- **SSH Honeypot**:
```bash
python3 honeypy.py -a 0.0.0.0 -p 2224 -u admin -pw secret --ssh
```
- **HTTP Honeypot**:
```bash
python3 honeypy.py -a 0.0.0.0 -p 5000 -u admin -pw password --http
```
**Notes**
By default, if no username/password is specified, the HTTP honeypot uses "admin" and "password".
Logs are saved in separate files for SSH and HTTP interactions in the root directory.