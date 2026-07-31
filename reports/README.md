# Reports

This directory contains the documentation and supporting experimental artifacts associated with the implementation and evaluation of Multipath QUIC (MPQUIC).

## Contents

### 1. MPQUIC_CNI_FINAL_REPORT.pdf

The final internship report documenting the implementation, validation, and experimental evaluation of MPQUIC.

---

### 2. MPQUIC_CNI_FINAL_REPORT.zip

The complete LaTeX source of the internship report, including all chapters, figures, bibliography, and supporting files required to regenerate the final PDF.

---

### 3. MPQUIC_CAPTURES_HEADERS.tar.zst.part_aa
### 4. MPQUIC_CAPTURES_HEADERS.tar.zst.part_ab
### 5. MPQUIC_CAPTURES_HEADERS.tar.zst.part_ac

These files together contain the packet captures used during the experimental evaluation presented in the report.

To reduce repository size, the original packet captures were processed to retain only the packet headers before being compressed using the Zstandard (`.tar.zst`) format. The compressed archive was subsequently split into multiple parts to comply with GitHub's recommended file size limits.

## Reconstructing the Packet Capture Archive

### Step 1: Combine the archive parts

```bash
cat MPQUIC_CAPTURES_HEADERS.tar.zst.part_* > MPQUIC_CAPTURES_HEADERS.tar.zst
```

### Step 2: Extract the archive

```bash
tar --zstd -xf MPQUIC_CAPTURES_HEADERS.tar.zst
```

This recreates the `MPQUIC_CAPTURES_HEADERS` directory containing the processed packet captures used for the experimental evaluation.

---

## Note

The packet captures contain only packet headers and protocol metadata. Packet payloads have been removed to significantly reduce storage requirements while preserving sufficient information for protocol analysis using tools such as Wireshark.
