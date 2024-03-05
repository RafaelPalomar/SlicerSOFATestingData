SlicerSOFA Testing Data Repository Guide
====================================

Purpose of the Repository
-------------------------

The SlicerSOFA Testing Data Repository is specifically established to manage the data used for testing purposes in the SlicerSOFA extension. It serves as the central hub for storing and organizing SlicerSOFA's testing assets.

Managing Data Using Content-Based Addressing
--------------------------------------------

Files are methodically managed within the repository by utilizing content-based addressing via [releases](https://github.com/rafaelpalomar/SlicerSOFATestingData/releases). Releases are named based on the hash algorithm employed in their creation.

For each predetermined hash algorithm `<HASHALGO>` (i.e., MD5, SHA256, etc.), please ensure the repository includes:

- A release under the name `<HASHALGO>`.
- A CSV file named `<HASHALGO>.csv`, featuring an enumerated list of `<hashsum>;<filename>` pairs.
- A markdown file `<HASHALGO>.md`, containing structured hyperlinks formatted as `* [<filename>](https://github.com/rafaelpalomar/SlicerSOFATestingData/releases/download/<HASHALGO>/<checksum>)`. Note that this markdown file is auto-generated after each upload based on the CSV file. Any changes, including deletions to files, should be reflected by editing the CSV file accordingly.

For consistency in execution, we advise performing the commands presented in this guide in the same terminal session. Please refer to the section "Documentation Conventions" for additional clarification.

Procedures for File Management
------------------------------

### Uploading Files:
1. Complete the installation of the [Prerequisites](#prerequisites).
2. Relocate the designated files to the `INCOMING` directory.
3. Run the `process_release_data.py` script with your GitHub token and the upload command:

   ```
   $ python process_release_data.py upload --github-token your_github_token_here
   ```

4. Following a successful upload, you have the option to empty the `INCOMING` directory.

### Downloading Files:
1. Confirm the [Prerequisites](#prerequisites) are in place.
2. Utilize the `process_release_data.py` script with your GitHub token, the download command, and the appropriate hash algorithm. Note that if there are several versions of a file, distinct filenames are automatically produced within the download directory by appending the checksum.

   ```
   $ python process_release_data.py download --github-token your_github_token_here
   ```

### Renaming a File:
To change the name of a file, the `<HASHALGO>.csv` file must be downloaded from the associated release, edited, and re-uploaded. Subsequently, initiate an upload process using the `process_release_data upload` command. Keep in mind that alteration of filenames does not affect the integrity of fetching or downloading the files due to the primary usage of hash sums for identification.

### Deleting a File:
To delete a file, begin by downloading the respective `<HASHALGO>.csv`, remove the relevant file entry, upload the modified CSV, and proceed with the `process_release_data upload`. Additionally, delete the file from the release assets.

Caution: File deletion is generally discouraged to preserve the integrity of past versions of software that may require access to the original data. Only consider deletion for files mistakenly uploaded.

Setting the Foundations (Prerequisites)
---------------------------------------

1. Clone the project repository to your local system:

   ```
   $ git clone git://github.com/rafaelpalomar/SlicerSOFATestingData
   ```

2. Install Python, followed by the [githubrelease](https://github.com/j0057/github-release#installing) package:

   ```
   $ pip install githubrelease
   ```

3. [Create a personal GitHub access token](https://help.github.com/articles/creating-an-access-token-for-command-line-use) and assign it "repo" level permissions. This token enables you to perform read and write operations within the repository.

Understanding Documentation Conventions
---------------------------------------

Commands intended for terminal execution are indicated with a dollar sign (`$`). Example:

```
$ echo "Hello"
Hello
```

The user is required to enter `echo "Hello"` in their terminal as indicated without the dollar sign.
