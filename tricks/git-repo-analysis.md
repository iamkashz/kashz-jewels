# git repo analysis

NOTE: if there is a `.git` directory, the master directory is a git repository.

## GitTools

### Finder

Find websites that expose `.git` publicly

```bash
gitfinder.py -i URL.txt -t [THREADS]
```

### DUMPER

Having known a `.git` directory exists, this tool can download the files related to the git-repo.

```bash
gitdumper.sh http://IP/PATH/.git/ FOLDER_NAME
```

### EXTRACTOR

**NOTE: if kali setup is `kashz-kali`; filename is `gitextractor.sh`**

When `gitdumper.py` downloads incomplete git repositories, this tool can be used to restore contents. The tool reads
the `.git/` and creates a new directory where the extracted files are saved.

```bash
extractor.sh FOLDER_NAME_CONTAINING_.git SOURCE_CODE_DIR

# only for kashz-kali
gitextractor.sh FOLDER_NAME_CONTAINING_.git SOURCE_CODE_DIR
```

## Reference

* [internetwache/GitTools](https://github.com/internetwache/GitTools)