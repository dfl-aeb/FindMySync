<div align="center">
  <p>
    <h3>
      <b>
        FindMySync
      </b>
    </h3>
  </p>
  <p>
    <b>
      Synchronize Apple FindMy data with Remote server
    </b>
  </p>
  <p>

  </p>
  <br />
  <p>

![FindMySync](./docs/screenshot.png)

  </p>
</div>

<details open>
  <summary><b>Table of contents</b></summary>

---

- [Features](#features)
- [Usage](#usage)
- [Contributing](#contributing)
- [Changelog](#changelog)
- [License](#license)

---

</details>

## **Homepage**



## **Features**

- Supporting both Devices and Items data, including iPhones, iPads, Airtags,...
- Synchronizing data with a custom endpoint, with Authorization header
- Supporting macOS Catalina 10.15 - Tahoe 26.0+
- Automatic BeaconStore key extraction for macOS Sequoia (15.0+) and Tahoe (26.0+)
- ...

**To suggest anything, please join our [Discussion board](https://github.com/MartinPham/FindMySync/discussions).**


## **Usage**
Check here [martinpham.com/findmysync](https://www.martinpham.com/findmysync/).

### **macOS Sequoia (15.0+) and Tahoe (26.0+) Support**

For macOS Sequoia and newer versions, the BeaconStore key extraction method has been updated to use the Service attribute instead of Label. The app will automatically attempt this method.

If automatic extraction fails, you may need to manually extract the key using [beaconstorekey-extractor](https://github.com/pajowu/beaconstorekey-extractor) and enter it in the Extras panel.


## **Contributing**

Please contribute using [GitHub Flow](https://guides.github.com/introduction/flow). Create a branch, add commits, and then [open a pull request](https://github.com/MartinPham/FindMySync/compare).

## **Changelog**

- **v1.3 / TBD**
  - Add macOS Sequoia (15.0+) and Tahoe (26.0+) support
  - Implement new BeaconStore key extraction method using Service attribute
  - Improved error messages and logging for key extraction
  - Add fallback methods for BeaconStore key retrieval
  - Fix [Issue #40](https://github.com/MartinPham/FindMySync/issues/40) - macOS Sequoia compatibility
  - Implementation based on [Issue #47](https://github.com/MartinPham/FindMySync/issues/47) and [beaconstorekey-extractor](https://github.com/pajowu/beaconstorekey-extractor)

- **v1.2 / 20240318-2212**
  - Add Sonoma 14.4 support (Thanks to [@YeapGuy](https://github.com/YeapGuy) and [@airy10](https://github.com/airy10))

## **License**

This project is licensed under the [GNU General Public License v3.0](https://opensource.org/licenses/gpl-3.0.html) - see the [`LICENSE`](LICENSE) file for details.
