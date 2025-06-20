# PDF Password Cracker

## Description

A robust Python-based tool designed to decrypt password-protected PDF files. This utility supports both wordlist attacks (using a predefined list of passwords) and brute-force generation of passwords based on specified character sets and lengths. It utilizes multithreading to speed up the cracking process.

## Features

  * **Wordlist Attack**: Attempt to decrypt PDFs using a provided list of common or known passwords.
  * **Brute-Force Generation**: Generate passwords on the fly based on a custom character set (letters, digits, symbols) and specified minimum/maximum lengths.
  * **Multithreading Support**: Utilizes `concurrent.futures.ThreadPoolExecutor` to perform parallel password attempts, significantly speeding up the cracking process.
  * **Progress Bar**: Provides a real-time progress indicator using `tqdm` during decryption attempts.
  * **Command-Line Interface**: Easy to use via command-line arguments.

## Prerequisites

Before running this script, ensure you have the following installed:

  * **Python 3.x**: Download from [python.org](https://www.python.org/).
  * **Required Python Libraries**: `pikepdf` and `tqdm`.

## Installation

1.  **Clone the repository**:

    ```bash
    git clone https://github.com/jagadaprarthana/python-pdf-cracker.git
    cd python-pdf-cracker
    ```

2.  **Install dependencies**:

    ```bash
    pip install -r requirements.txt
    ```

## Usage

The `cracker.py` script can be used in two main modes: with a wordlist, or by generating passwords on the fly.

### Mode 1: Using a Wordlist

To crack a PDF using a predefined list of passwords:

```bash
python3 cracker.py <pdf_file_path> --wordlist <wordlist_file_path> [--max_workers <number_of_threads>]
```

  * `<pdf_file_path>`: Path to the password-protected PDF file.
  * `<wordlist_file_path>`: Path to your text file containing passwords (one password per line).
  * `--max_workers <number_of_threads>`: (Optional) Number of parallel threads to use (default is 4).

**Example:**

```bash
python3 cracker.py encrypted_document.pdf --wordlist common_passwords.txt --max_workers 8
```

### Mode 2: Generating Passwords (Brute-Force)

To generate passwords on the fly based on a character set and length:

```bash
python3 cracker.py <pdf_file_path> --generate [--min_length <min_len>] [--max_length <max_len>] [--charset <characters>] [--max_workers <number_of_threads>]
```

  * `<pdf_file_path>`: Path to the password-protected PDF file.
  * `--generate`: Flag to activate password generation mode.
  * `--min_length <min_len>`: (Optional) Minimum length of passwords to generate (default is 1).
  * `--max_length <max_len>`: (Optional) Maximum length of passwords to generate (default is 3).
  * `--charset <characters>`: (Optional) String of characters to use for generation (default includes `ascii_letters`, `digits`, `punctuation`).
  * `--max_workers <number_of_threads>`: (Optional) Number of parallel threads to use (default is 4).

**Important Notes for Brute-Force:**

  * Generating passwords can be **extremely time-consuming** for longer lengths or larger character sets. Be mindful of the `--min_length`, `--max_length`, and `--charset` settings. For example, `max_length=5` with the default `charset` can take a very long time.
  * The default `max_length` is set to 3 for demonstration purposes. Increase it cautiously.

**Example (generating short, all-lowercase passwords):**

```bash
python3 cracker.py secret.pdf --generate --min_length 1 --max_length 4 --charset abcdefghijklmnopqrstuvwxyz --max_workers 4
```

## How it Works

The script attempts to open the PDF with various passwords. It leverages `pikepdf` for PDF manipulation and `tqdm` for progress visualization. Multithreading is implemented using `concurrent.futures.ThreadPoolExecutor` to concurrently try multiple passwords, which can significantly reduce the decryption time, especially on multi-core processors.

## License

This project is licensed under the [MIT License](https://www.google.com/search?q=LICENSE) - see the `LICENSE` file for details.

## Disclaimer

This tool is intended for educational purposes and ethical use only, such as recovering passwords for your own forgotten documents. Misuse of this tool for unauthorized access to PDF files is illegal and unethical. The author is not responsible for any misuse.
