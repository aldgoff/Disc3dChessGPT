<details open> <summary>**1️⃣ Rename filenames (spaces → underscores)**</summary>

Goal: make every .png filename safe and uniform.

# Dry run first
rename -n 's/ /_/g' *.png

# If output looks right
rename 's/ /_/g' *.png
# or if 'rename' isn't installed:
for f in *.png; do nf="${f// /_}"; [ "$f" != "$nf" ] && mv "$f" "$nf"; done


✅ Double-check

ls | grep " "           # should print nothing
find . -type f -name "* *"


When clean, collapse this and expand Step 2.

</details>
<details> <summary>**2️⃣ Refresh metadata (.DS_Store)**</summary>
rm -f .DS_Store


macOS will regenerate it automatically.

Then expand Step 3.

</details>
<details> <summary>**3️⃣ Generate ordered list of PNGs**</summary>
ls -1 *.png | sort > ordered_figures_list.txt
wc -l ordered_figures_list.txt   # expect 264


Then expand Step 4.

</details>
<details> <summary>**4️⃣ Build new manifest**</summary>

Use your latest good manifest as a base; replace filenames and rebuild URLs:

https://raw.githubusercontent.com/aldgoff/Disc3dChessGPT/main/figures/<filename>.png


Confirm:

264 total figures

Captions/descriptions non-empty

URLs open directly in browser

Then expand Step 5.

</details>
<details> <summary>**5️⃣ Upload manifest to Builder**</summary>

Rename file to what Builder expects (e.g., figures_manifest_all_withURL_safe.json).

Upload → reload manifest → manifest status.
Expect: 264 figures, all captions/descriptions non-empty.

Test render:

show figure 2
show figure 13
show figure 15


Then expand Step 6.

</details>
<details> <summary>**6️⃣ Clean and re-populate GitHub repo**</summary>
cd Disc3dChessGPT/figures
git rm -r .
cp /path/to/renamed/files/*.png .
git add .
git commit -m "Canonicalize figure filenames (spaces→underscores)"
git push


Double-check

ls | grep " "    # none
git status       # clean


Then expand Step 7.

</details>
<details> <summary>**7️⃣ Verify limits and repo view**</summary>

GitHub → figures/ folder shows 264 PNGs.

Clicking each displays properly.

No “too many files” warnings (limit ≫ 264).

Then expand Step 8.

</details>
<details> <summary>**8️⃣ Final Builder test**</summary>
reload manifest
manifest status
show figure 15


✅ All images render inline, URLs have underscores only.

Then expand Step 9.

</details>
<details> <summary>**9️⃣ Archive old versions (tag)**</summary>
git tag -a v1.0_pre_rename -m "Before filename canonicalization"
git push origin v1.0_pre_rename


You now have a reproducible, stable, future-proof baseline.
🎯 Done.

</details>
