<img src="assets/logo.png" width="112" height="112" alt="RasterBytes logo">

# RasterBytes

Estimate uncompressed raster storage with aligned scanlines. This Blyx library is part of the documents, images and media collection.

Encoded file size gives a poor estimate of decoded thumbnail memory. Account for output dimensions and scanline padding before allocating. [Pillow, aspect-preserving containment](https://pillow.readthedocs.io/en/stable/reference/ImageOps.html#PIL.ImageOps.contain)

## Install and run

Install [Blyx 0.2.1](https://www.blyx-lang.space/download) with a Rust toolchain and host linker for native builds.

```sh
git clone --depth 1 --branch v0.1.0 https://github.com/Rahulchaube1/blyx-rasterbytes.git
cd blyx-rasterbytes
blyxc native-run example.blyx
blyxc native-run tests.blyx
```

[Run the editable browser example](https://www.blyx-lang.space/play?example=package-rasterbytes) · [Package page](https://www.blyx-lang.space/packages/rasterbytes) · [Handbook](https://doc.blyx-lang.space/guide/hoopoe)

## Import the module

Run this in the directory containing your application's entry file.

```sh
git clone --depth 1 --branch v0.1.0 https://github.com/Rahulchaube1/blyx-rasterbytes.git vendor/rasterbytes
```

```blyx
use vendor::rasterbytes::rasterbytes;

fn main() {
    let width = 3.0;
    let height = 2.0;
    let channels = 3.0;
    let alignment = 4.0;
    let result = rasterbytes_storage(width, height, channels, alignment);
    if len(result) == 0 { println!("invalid"); return; }
    let mut i = 0;
    while i < len(result) {
        println!(at(result, i));
        i += 1;
    }
}
```

Expected output

```text
9
12
24
```

## API

`rasterbytes_storage(width, height, channels, alignment)`

Returns [bytes per unpadded row, aligned stride, total bytes]. Each channel takes one byte. Counts must stay in the exact integer range. Invalid arguments and nonfinite results return an empty vector. Integers carried in numeric vectors use the exact range from −(2^53−1) to 2^53−1.

| Argument | Domain |
| --- | --- |
| width | A positive exact integer |
| height | A positive exact integer |
| channels | A positive exact integer |
| alignment | A positive exact integer |

## In use

[Hoopoe](https://github.com/Rahulchaube1/blyx-hoopoe) uses this module to plan a thumbnail and check the decoded pixel buffer against a byte budget.

## Verification and contributions

The regression suite in [tests.blyx](tests.blyx) checks the example, boundary cases and invalid inputs. Include a short reproducer and your compiler version in [an issue](https://github.com/Rahulchaube1/blyx-rasterbytes/issues). The source is dual-licensed under [MIT](LICENSE-MIT) or [Apache-2.0](LICENSE-APACHE). The package artwork uses [Lucide icons](https://lucide.dev/license); see [artwork notices](assets/NOTICE.txt).

## Connect with Rahul Chaube

[Portfolio](https://www.rahulchaube1.com/) · [GitHub](https://github.com/Rahulchaube1) · [LinkedIn](https://www.linkedin.com/in/rahulchaube1) · [Hugging Face](https://huggingface.co/oncody) · [X](https://x.com/RahulChaube_) · [EverestQ](https://www.everestqai.com/) · [Contact](https://www.rahulchaube1.com/contact)

[Blyx website](https://www.blyx-lang.space/) · [BlyxTorch](https://www.blyx-lang.space/packages/blyxtorch) · [Handbook](https://doc.blyx-lang.space/) · [Community](https://www.blyx-lang.space/community)

Support Rahul’s open-source work through [GitHub Sponsors](https://github.com/sponsors/Rahulchaube1) or [Buy Me a Coffee](https://buymeacoffee.com/rahulchaube).
