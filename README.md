# ImpactTube

ImpactTube é uma distribuição personalizada baseada no [NewPipe](https://github.com/TeamNewPipe/NewPipe/), preservando os créditos dos criadores originais no aplicativo, especialmente na seção Sobre. O projeto mantém a licença GPL-3.0-or-later e usa GitHub Actions para gerar APKs Debug em pushes/PRs e Release unsigned sob demanda ou na branch principal.

## Build local

Requer JDK 21 e Android SDK configurado:

```bash
./gradlew assembleDebug
./gradlew assembleRelease
```

Os APKs ficam em `app/build/outputs/apk/`. O workflow `Build ImpactTube APK` publica os artefatos automaticamente.

## Produto

A direção UX aprovada é tema escuro premium com identidade musical e materialidade claymorphism refinada. Consulte [`docs/PRODUCT-DIRECTION.md`](docs/PRODUCT-DIRECTION.md).
