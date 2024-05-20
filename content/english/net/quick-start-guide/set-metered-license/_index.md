---
title: Set Metered License
linktitle: Set Metered License
second_title: GroupDocs.Editor .NET API
description: 
type: docs
weight: 12
url: /net/quick-start-guide/set-metered-license/
---

## Complete Source Code
```csharp
using System;

namespace GroupDocs.Editor.Examples.CSharp.QuickStart
{
    /// <summary>
    /// This example demonstrates how to set Metered license.
    /// Learn more about Metered license at https://purchase.groupdocs.com/faqs/licensing/metered.
    /// </summary>
    class SetMeteredLicense
    {
        public static void Run()
        {
            string publicKey = "*****";
            string privateKey = "*****";

            Metered metered = new Metered();
            metered.SetMeteredKey(publicKey, privateKey);

            Console.WriteLine("License set successfully.");
        }
    }
}
```
