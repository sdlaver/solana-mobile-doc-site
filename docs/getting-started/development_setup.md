import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';
import Card from "../../src/components/Card"
import CardLayout from "../../src/layouts/CardLayout"

# Development Setup

This quickstart guide will demonstrate how to quickly install necessary tools and set up your development environment, getting you ready to start
building a mobile app on Solana. 

### Android Device/Emulator

:::note
You don't need a Saga device or physical device to build on Solana Mobile! The Mobile Wallet Adapter SDK is compatible with any android device.
:::

To start building with the Solana Mobile SDK, you need an android device or emulator. You can follow the official [Android developer documentation](https://developer.android.com/studio/run/emulator)
for this step.

You will also most likely want to download [Android Studio](https://developer.android.com/studio) to build apps and manage your device.

### Install a wallet app

The [Mobile Wallet Adapter](https://github.com/solana-mobile/mobile-wallet-adapter) library allows your dApp to connect and interface with Wallet Apps that implement the Mobile Wallet Adapter protocol. For testing, you want to have a MWA-compatible wallet on the same device/emulator as your dApp.

#### fakewallet

The [fakewallet](https://github.com/solana-mobile/mobile-wallet-adapter/tree/main/android/fakewallet) app is a test implementation of a Solana wallet app compatible with 
the Mobile Wallet Adapter SDK. It doesn't store persistent keypairs and the wallet is "reset" each time the app is exited.

<details>
<summary>Installation steps</summary>

1. Clone the Mobile Wallet Adapter repo, containing the fakewallet app from the [github repository](https://github.com/solana-mobile/mobile-wallet-adapter)

```
git clone https://github.com/solana-mobile/mobile-wallet-adapter.git
```

2. In Android Studio, `Open project > Navigate to the cloned directory > Select mobile-wallet-adapter/android/build.gradle`

3. After Android Studio finishes loading the project, select `fakewallet` in the build/run configuration dropdown in the top right

4. Make sure you have your created Android emulator or connected your physical device. If not, you can follow setup instructions from the previous section.

5. You should now be able to see the fakewallet app on your Android device.

6. Now you can use the Mobile Wallet Adapter SDK to connect your dApp to the fakewallet app and test your integration.

</details>

#### Production

Fakewallet was created for implementation reference and quick testing purposes. For production testing, test your dApp with popular MWA-compatible wallet apps like [Phantom](https://play.google.com/store/apps/details?id=app.phantom) and [Solflare](https://play.google.com/store/apps/details?id=com.solflare.mobile).

### Choose a development framework

Currently, the Solana Mobile SDK can be installed as a dependency for apps built in React Native and Android Native. In the future, there will be support for additional frameworks like React Native Expo, Flutter/Dart.

<CardLayout>
    <Card
        to="/react-native/quickstart"
        header={{
            label: "React Native Setup",
            translateId: "react-native-setup",
        }}
        body={{
            label: "Quickly set up a React Native Android project with our Mobile Wallet Adapter Javascript SDK.",
            translateId: "react-native-setup-body",
        }}
    />
    <Card
        to="/android-native/quickstart"
        header={{
            label: "Android Native Setup",
            translateId: "android-native-setup",
        }}
        body={{
            label: "Quickly set up a Native Android project with our Mobile Wallet Adapter SDK in Java or Kotlin.",
            translateId: "android-native-setup-body",
        }}
    />
</CardLayout>





