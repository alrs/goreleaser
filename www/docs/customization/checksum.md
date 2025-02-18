# Checksums

GoReleaser generates a `project_1.0.0_checksums.txt` file and uploads it with the
release, so your users can validate if the downloaded files are correct.

The `checksum` section allows customizations of the filename:

```yaml
# .goreleaser.yaml
checksum:
  # You can change the name of the checksums file.
  # Default is `{{ .ProjectName }}_{{ .Version }}_checksums.txt`.
  name_template: "{{ .ProjectName }}_checksums.txt"

  # Algorithm to be used.
  # Accepted options are sha256, sha512, sha1, crc32, md5, sha224 and sha384.
  # Default is sha256.
  algorithm: sha256

  # IDs of artifacts to include in the checksums file.
  # If left empty, all published binaries, archives, linux packages and source archives
  # are included in the checksums file.
  # Default is an empty list.
  ids:
    - foo
    - bar

  # Disable the generation/upload of the checksum file.
  # Default is false.
  disable: true

  # You can add extra pre-existing files to the checksums file.
  # The filename on the checksum will be the last part of the path (base).
  # If another file with the same name exists, the last one found will be used.
  # These globs can also include templates.
  #
  # Defaults to empty.
  extra_files:
    - glob: ./path/to/file.txt
    - glob: ./glob/**/to/**/file/**/*
    - glob: ./glob/foo/to/bar/file/foobar/override_from_previous
    - glob: ./single_file.txt
      name_template: file.txt # note that this only works if glob matches 1 file only


  # Additional templated extra files to add to the checksum.
  # Those files will have their contents pass through the template engine,
  # and its results will be added to the checksum.
  #
  # Default: empty
  # Since: v1.17 (pro)
  # This feature is available in only GoReleaser Pro.
  templated_extra_files:
    - src: LICENSE.tpl
      dst: LICENSE.txt

```

!!! tip
    Learn more about the [name template engine](/customization/templates/).
