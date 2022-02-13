# Cryptography
 
Closely related to my Applied Math [topics](https://github.com/mstrielnikov/Math) (Computer Math and Cryptography) which could be a solid theoretical background.

## Modulo Ring Cryptography & RSA
* [Medium: Cryptosystems Based on Composite Degree Residuosity Classes and Paillier Encryption](https://medium.com/asecuritysite-when-bob-met-alice/in-a-world-of-privacy-the-time-has-come-for-paillier-encryption-to-step-forward-bea8e701f3c3)
* [Medium: Camenisch-Shoup Verifiable Encryption using Kryptology](https://medium.com/asecuritysite-when-bob-met-alice/camenisch-shoup-verifiable-encryption-using-kryptology-and-golang-fba70e05727a) - GoLang
* [Medium: RSA Accumulators And Proving Knowledge](https://medium.com/asecuritysite-when-bob-met-alice/rsa-accumulators-and-proving-knowledge-c63bdb8817b8) - GoLang
* [Asecurity: RSA implementation](https://asecuritysite.com/rust/rsa02) - Rust
* [Asecurity: RSA implementation (with big integers)](https://asecuritysite.com/rust/rsa01) - Rust
* [Asecurity: integer factorization](https://asecuritysite.com/rust/factors?n=653764321953243) and [sample](https://asecuritysite.com/encryption/rsac) - Rust

## Ellyptical Curves Cryptography (ECC)
* [Choose safe curves for application](https://safecurves.cr.yp.to/) - Very Usable Application
* [Technical Guideline BSI TR-03111](https://www.bsi.bund.de/SharedDocs/Downloads/EN/BSI/Publications/TechGuidelines/TR03111/BSI-TR-03111_V-2-1_pdf.pdf?__blob=publicationFile&v=1) - Whitepaper
* [Wikipedia: Elliptic Crypography Overwiew](https://en.wikipedia.org/wiki/Elliptic-curve_cryptography)
* [Habr: Popular intro in ECC](https://habr.com/ru/post/335906/)
* [Medium: MOV-attack](https://medium.com/asecuritysite-when-bob-met-alice/cracking-elliptic-curves-with-the-mov-attack-b5ea00dcc939) - GoLang
* [Medium: Add and Removing Data from ECC Accumulators](https://billatnapier.medium.com/add-and-removing-data-from-ecc-accumulators-a459b97262de)
* [Medium: The Order in ECC](https://medium.com/asecuritysite-when-bob-met-alice/whats-the-order-in-ecc-ac8a8d5439e8)
* [Asecurity: MOV-attack using Kryptology](https://asecuritysite.com/kryptology/mov?a=50) - GoLang
* [Asecurity: Matchig random value to a curve](https://asecuritysite.com/encryption/tocurve) - Python
* [Asecurity: ECC programmatic implementations](https://asecuritysite.com/ecc/)

## Edward's Curves Cryptography (Ed25519 & Ed448)
* [Edward's curves research](https://core.ac.uk/download/pdf/146445895.pdf) - Monography
* [HAL archives: Edward's curves](https://hal.archives-ouvertes.fr/hal-01942759/document) - Whitepaper
* [Things that use Curve25519](https://ianix.com/pub/curve25519-deployment.html)
* [Medium: Ed25519 and Ed448](https://medium.com/asecuritysite-when-bob-met-alice/towards-web3-ed25519-ed448-and-ed2551-dilithium-32d36b06f499) - GoLang
* [Medium: Usage of Ed25519 (crate Crypto)](https://medium.com/asecuritysite-when-bob-met-alice/curve-25519-and-rust-4d3a3e379887) - Rust
* [Asecurity: Usage of Ed25519 (author's crate)](https://asecuritysite.com/rust/rust_ed25519) - Rust
* [Asecurity: Usage of curve25519 (multi languages programmatic implementations)](https://asecuritysite.com/curve25519)
* [Asecurity: Schnorr signature](https://asecuritysite.com/rust/rust_schnorr) - Rust
* [Asecurity: scalar inverse of Curve25519 (Montgomery)](https://asecuritysite.com/rust/rust_mont25519inv) - Rust
* [Asecurity: scalar inverse on Ed25519 (Edwards)](https://asecuritysite.com/rust/rust_ed25519inv) - Rust
* [Asecurity: ElGamal Protocol with Ed25519](https://asecuritysite.com/kryptology/elgamal01) - GoLang
* [Asecurity: Distributed key generation (DKG) using FROST threshold Schnorr signature protocol in Kryptology](https://asecuritysite.com/kryptology/dkg) - GoLang
* [Asecurity: recrypt - lib for proxy encryption with Ed25519](https://asecuritysite.com/rust/rust_transform) - Rust

## Digital Signatures
* [Cryptowiki: Digital Signature basics and application](http://cryptowiki.net/index.php?title=Слепая_электронная_подпись_и_ее_применения)

## Password authenticated key exchange (PAKE)
* [Asecurity: OPAQUE protocol](https://asecuritysite.com/encryption/op) - GoLang
* [Asecurity: Encode hash on elliptic curve](https://asecuritysite.com/circl/circl_hashto) - GoLang

## Pairing based cryptography (PBC)
* [An Introduction to Pairing-Based Cryptography](https://www.math.uwaterloo.ca/~ajmeneze/publications/pairings.pdf) - Whitepaper
* [Wikipedia: PBC intro](https://en.wikipedia.org/wiki/Pairing-based_cryptography)
* [Secret Double Octopus: PBC intro](https://doubleoctopus.com/security-wiki/encryption-and-cryptography/pairing-based-cryptography/)
* [Medium: BLS signatures](https://medium.com/asecuritysite-when-bob-met-alice/bls-signatures-fast-efficient-and-short-checked-with-the-magic-of-crypto-pairing-c63d17a38278) - GoLang
* [Medium: Towards Zero (Knowledge): Pairing-based Cryptography using CIRCL](https://medium.com/asecuritysite-when-bob-met-alice/towards-zero-knowledge-pairing-based-cryptography-using-circl-11b2bd531c92) - GoLang
* [Asecurity: PBC sample with Kryptology framework](https://asecuritysite.com/kryptology/pairing) - GoLang
* [Asecurity: Encrypted search using crypto pairing with MIRACL](https://asecuritysite.com/rust/rust_miracl02) - Rust
* [Asecurity: Searching for Encrypted Data with Identity Based Encryption (IBE)](https://asecuritysite.com/pairing/mir_ibe_search) - GoLang

## Homomorphic Encryption
* [Fully Homomorphic Encryption over the Integers](https://eprint.iacr.org/2009/616.pdf) - Whitepaper
* [IBM: Homomorphic encryption tool for Linux](https://habr.com/ru/company/dcmiran/blog/513388/)
* [Medium: Homomorphic encryption using ElGamal](https://billatnapier.medium.com/homomorphic-addition-and-subtraction-using-elgamal-3fa91be249a6) - GoLang
* [Medium: Homomorphic encryption sample with Kryptology](https://billatnapier.medium.com/towards-total-encryption-5fc11c7ce3e1) - GoLang
* [Asecurity: Lattice based cryptography](https://asecuritysite.com/encryption/go_lattice_cc5) -GoLang

## Post quantum Cryptography
* [Wikipedia: List of Post Quantum Cryptography](https://en.wikipedia.org/wiki/Post-quantum_cryptography)
* [Wikipedia: Lattice-based cryptography](https://en.wikipedia.org/wiki/Lattice-based_cryptography)
* [Medium: General Overwiew](https://billatnapier.medium.com/post-quantum-lattice-polynomials-and-modulo-afaa9caf8aa5)
* [Habr: NIST competitors as a Post Quantum standards](https://habr.com/ru/post/512410/)
* [Asecurity: NTRU](https://asecuritysite.com/encryption/ntru_key)
* [Asecurity: Multivariative cryptography](https://asecuritysite.com/encryption/multiv2)
* [Asecurity: SIKE (Supersingular Isogeny Key Encapsulation)](https://asecuritysite.com/encryption/sike)
* [Asecurity: SIKE (Supersingular Isogeny Key Encapsulation) for KEM](https://asecuritysite.com/circl/circl_sike)
* [Asecurity: Kyber and SIKE PQC Key Exchange Mechanism (KEM) with CIRCL](https://asecuritysite.com/circl/circl_kyber)

## Quantum Cryptography
* [Habr: Quantum Hashing](https://habr.com/ru/company/yandex/blog/312072/)

## Secret sharing protocols
* [Wikipedia: Shamir secret sharing](https://en.wikipedia.org/wiki/Shamir%27s_Secret_Sharing)

## Zero-knowledge proof & protocols
* [Medium: Rust implementation of Zero-proof example](https://medium.com/asecuritysite-when-bob-met-alice/proving-you-know-answer-to-a-quadratic-equation-without-giving-the-answer-using-rust-crypto-a1d14228b5bd)
* [Medium: HVZK (Honest Verifier Zero Knowledge) For RSA and Using Kryptology](https://medium.com/asecuritysite-when-bob-met-alice/hvzk-honest-verifier-zero-knowledge-for-rsa-and-using-kryptology-e0f1aa86c24e)
* [Asecurity: ZeroKnowledge proof using Kryptology](https://asecuritysite.com/kryptology/zk?x=7&a=-1&b=-42) - GoLang
* [Asecurity: Verifiable Delay Function (VDF)](https://asecuritysite.com/principles/vdf) - GoLang

## Hashes and One-Way Functions
* [Medium: Length extension attack](https://billatnapier.medium.com/the-weaknesses-of-md5-sha1-and-sha-256-the-length-extension-attack-4e5902fb4ae4?sk=682294f4ce1bcd673997e0c546da2cc0) - Python
* [Medium: Key Wrapping](https://medium.com/asecuritysite-when-bob-met-alice/how-do-we-protect-an-encryption-key-meet-key-wrapping-25a0676a73c6) - GoLang

## Pseudo Random Generators
* [Medium: Verifiable Oblivious Pseudorandom Functions](https://medium.com/asecuritysite-when-bob-met-alice/we-give-away-too-many-of-our-digital-secrets-heres-verifiable-oblivious-pseudorandom-functions-13ba5f78380f?source=friends_link&sk=27d57da266c7fb50d5c2292fe1d2fa89)

## Symmetric Encryption Protocols (AEAD, HMAC, MAC)
* [AEAD](https://www.engineering.iastate.edu/~daji/seminar/papers/R02.ACMCCS.pdf) - White papers
* [Medium: Poly1305-ChaCha20](https://medium.com/asecuritysite-when-bob-met-alice/chacha20-and-rust-353c2f5b363) - Rust
* [Medium: HMAC-SHA256](https://medium.com/asecuritysite-when-bob-met-alice/hkdf-sha256-and-rust-fe23abde28f0) - Rust
* [Medium: AEAD sample and intro](https://medium.com/asecuritysite-when-bob-met-alice/so-what-is-aead-and-why-is-it-so-important-for-encryption-8e2bf16eed6f) - Rust

## Symmetric Ciphers
* [Soatok blog: Symmetric encryption](https://soatok.blog/2020/07/12/comparison-of-symmetric-encryption-methods/)
* [Asecurity: ChaCha20](https://asecuritysite.com/encryption/go_chacha) for [Golang](https://pkg.go.dev/golang.org/x/crypto/chacha20poly1305)
* [Medium: Rust implementation of ChaCha20 extended](https://medium.com/asecuritysite-when-bob-met-alice/96-bit-nonces-too-small-try-xchacha20-and-rust-b773bb8c9bff) - Rust

## End-to-end (E2E) security
* [Forward Secrecy](https://en.wikipedia.org/wiki/Forward_secrecy)
* [Signal papers: Double Ratchet algorithm](https://valsamaras.medium.com/the-signal-protocol-and-the-double-ratchet-algorithm-e3d01d1e403f)
* [Developer's blog: Noise Framework - intro](https://duo.com/labs/tech-notes/noise-protocol-framework-intro)
* [Noise Framework: Docs](https://noiseprotocol.org/) - Whitepapers
* [Cryptowiki: Noise framework](http://cryptowiki.net/index.php?title=Noise_Protocol_Framework)
* [Medium: The MALICIOUS framework: Tweakable Block Ciphers](https://medium.com/asecuritysite-when-bob-met-alice/the-malicious-framework-tweakable-block-ciphers-ec1823077da5)

## TLS
* [Tprogger: TLS](https://tproger.ru/articles/tls-handshake-explained/)
* [Xaker: OpenSSL and OpenSSH advanced usage](https://xakep.ru/2012/10/29/hardcore-openssh-and-openssh/) - Guide
* [TLS 1.3 Some explanatios](https://tls.dxdt.ru/protocol-1.3.html)

## I2P
* [Habr: I2P](https://habr.com/ru/company/itsoft/blog/552072/?utm_source=telegram&utm_medium=social&utm_campaign=/ru/company/itsoft/blog/552072/)
* [Habr: ECIES-X25519-AEAD-Ratchet for I2P](https://m.habr.com/ru/post/504610/)

## Libraries & frameworks
* [Asecurity: Cryptography samples](https://asecuritysite.com/encryption/)
* [Asecurity: Rust Crypto libraries](https://asecuritysite.com/rust/)
* [Asecurity: GoLang Crypto libraries](https://asecuritysite.com/golang)
* [Asecurity: Tink - GoLang cryptographic framework by Google](https://asecuritysite.com/tink)
* [Asecurity: Kryptology - GoLang Cryptographic framework by CoinBase](https://asecuritysite.com/kryptology/)
* [Asecurity: CIRCL - GoLang Cryptographic framework by CloudFlare](https://asecuritysite.com/circl)
* [Asecurity: MIRACL - Cryptographic Library for ECC and PBC (multiple language implementations including Go and Rust)](https://asecuritysite.com/miracl/)

## Resources
* [Security Double Octopus: Security wiki](https://doubleoctopus.com/security-wiki/#security-wiki-content)
* [OWASP: Cryptographic failures](https://owasp.org/Top10/A02_2021-Cryptographic_Failures/)
* [Infosec](https://github.com/vlsergey/infosec) - Books & lectures
* [Practical Cryptography](https://cryptobook.nakov.com)
* [GitHub: Useful cryptographic samples](https://github.com/gtank/cryptopasta) - GoLang

## Scripts
* [Eax blog: Practical cryptography and large arifmetics examples](https://eax.me/elliptic-curves-crypto/)
* [RSA CTF tool](https://github.com/Ganapati/RsaCtfTool)
* [Habr: GOST like protocol example](https://habr.com/ru/post/452200/)
* [RFC 7748: Elliptic Curves for Security](https://tools.ietf.org/html/rfc7748)
* [Asecurity: Bleichenbacher's attack](https://asecuritysite.com/encryption/c_c3)

## Books
* [Introduction to Elliptic Curves and Modular Forms](http://www.ega-math.narod.ru/Books/Koblitz.htm)
* [Schnorr](http://apmi.bsu.by/assets/files/agievich/schnorr.pdf)
