---
layout: default
title: Difference between Apple certificates(macOS)
comments: true
---

# Difference between Apples different certificates(macOS)

To distribute mac app outside app store, you need `Developer ID Installer` certificate.
To subbmit your app to app store, you need `Mac Installer Distribution` certificate.

>All team members can create their own development certificate. Only a team agent or admin can create a distribution certificate. Only a team agent can create a Developer ID certificate.

Certificate type | Certificate name | Description
--- | --- | ---
iOS Development | iPhone Developer: Team Member Name | Used to run an iOS, tvOS, or watchOS app on devices and use certain app services during development.
iOS Distribution | iPhone Distribution: Team Name | Used to distribute your iOS, tvOS, or watchOS app on designated devices for testing or to submit it to the store.
Mac Development | Mac Developer: Team Member Name | Used to enable certain app services for a Mac app during development and testing.
Mac App Distribution | 3rd Party Mac Developer Application: Team Name | Used to sign a Mac app before submitting it to the Mac App Store.
Mac Installer Distribution | 3rd Party Mac Developer Installer: Team Name | Used to sign and submit a Mac Installer Package, containing your signed app, to the Mac App Store.
Developer ID Application | Developer ID Application: Team Name | Used to sign a Mac app before distributing it outside the Mac App Store.
Developer ID Installer | Developer ID Installer: Team Name | Used to sign and distribute a Mac Installer Package, containing your signed app, outside the Mac App Store.
