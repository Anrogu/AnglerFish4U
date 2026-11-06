# 🎣 Anglerfish Readme Action
 
A GitHub Action written in Rust that generates a fully animated pixel art anglerfish (complete with glowing lure, breathing effects, and rising bubbles) whose colors dynamically adapt to your top GitHub programming languages based on your public repositories!
 
## ✨ Features
 
- **Dynamic Language Palette:** Automatically fetches your repository language statistics using the GitHub API and maps your top 3 languages directly onto the anglerfish's body, glowing lure, and fins using official GitHub Linguist hex colors.
- **Pure Rust Performance:** Compiles and executes in seconds thanks to a lightweight Rust binary.
- **Dual Output:** Generates both a fully compatible animated GIF (`anglerfish.gif`) for seamless rendering inside Markdown tables and an SVG version (`anglerfish.svg`).
- **Profile Integration:** Automatically updates your profile `README.md` with your top language and assets.
## 🚀 How to Use It in Your Profile
 
Add this workflow file to `.github/workflows/anglerfish.yml` in your GitHub profile repository (`your-username/your-username`):
 
```yaml
name: Generate Anglerfish Profile Art
 
on:
  schedule:
    - cron: "0 0 * * *" # Runs daily at midnight UTC
  workflow_dispatch:     # Allows manual triggers from the Actions tab
 
permissions:
  contents: write
 
jobs:
  update-anglerfish:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4
 
      - name: Run Anglerfish Action
        uses: Anrogu/AnglerFish4U
        with:
          github_username: ${{ github.repository_owner }}
          github_token: ${{ secrets.GITHUB_TOKEN }}
 
      - name: Commit and push changes
        run: |
          git config user.name "github-actions[bot]"
          git config user.email "github-actions[bot]@users.noreply.github.com"
          git add anglerfish.svg anglerfish.gif README.md
          git diff --staged --quiet || git commit -m "chore: update language anglerfish"
          git push
```
 
## 📌 README.md Setup
 
To display the anglerfish neatly next to your GitHub stats cards with a clean dividing line, paste this table into your profile `README.md`:
 
```html
<table>
  <tr>
    <td align="center" valign="middle">
      <img height="200" src="https://streak-stats.demolab.com/?user=YOUR_USERNAME&theme=react&hide_border=true" alt="GitHub Streak" />
    </td>
    <td align="center" valign="middle">
      <!-- MOST_USED_LANGUAGE_START -->
      <b>my most used language: <code>Java</code></b>
      <!-- MOST_USED_LANGUAGE_END -->
      <br /><br />
      <img height="150" src="./anglerfish.gif" alt="Language Pixel Art Anglerfish" />
    </td>
  </tr>
</table>
```
 
The action rewrites everything between the `MOST_USED_LANGUAGE_START` and `MOST_USED_LANGUAGE_END` markers on each run, so keep both comments in place.
 
## ⚙️ Action Inputs
 
| Input             | Description                                      | Required | Default                           |
| ----------------- | ------------------------------------------------ | -------- | --------------------------------- |
| `github_username` | Your GitHub handle to fetch language bytes       | Yes      | `${{ github.repository_owner }}`  |
| `github_token`    | Personal access token or `secrets.GITHUB_TOKEN`  | No       | `${{ github.token }}`             |
| `svg_out`         | File path for the generated SVG output           | No       | `anglerfish.svg`                  |
| `gif_out`         | File path for the generated GIF output           | No       | `anglerfish.gif`                  |
| `readme_path`     | Target Markdown file to update                   | No       | `README.md`                       |
 
## 🛠️ Built With
 
- **[Rust](https://www.rust-lang.org/)** – High-performance systems logic and data processing.
- **[reqwest](https://crates.io/crates/reqwest) & [serde](https://serde.rs/)** – Fast REST API consumption and JSON parsing.
- **[gif](https://crates.io/crates/gif) crate** – Custom frame-by-frame GIF encoder with full transparency and background disposal support.
## 📜 License
 
Distributed under the MIT License. Feel free to fork, modify, and use it to customize your developer profile!
