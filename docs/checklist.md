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
Goal: Ensure Finder has up-to-date layout info before reading file order.

1. Remove any stale .DS_Store files from the current folder and subfolders:

find . -name ".DS_Store" -delete

2. Open the “figures” folder in Finder

Switch to Icon View (⌘-1).

Arrange icons exactly the way you want them represented in the manifest (column-by-row layout).

Wait a few seconds — Finder automatically regenerates a fresh .DS_Store for that directory.

Close the window.

3. Verify regeneration:

ls -a | grep DS_Store

You should see .DS_Store listed.
If not, reopen Finder → adjust view once → close again.

Then continue to Step 3.

</details>
<details> <summary>**3️⃣ Generate ordered list of PNGs**</summary>

1. Capture DS_Store.

~~pip install ds_store~~

python3 -m ds_store ./.DS_Store > ds_output.txt

2. Sort in col/row order, pipe to a file.

perl -ne 'if(/^(.*?)\s+Iloc\s+\((\d+),\s*(\d+)\)/){printf "%s %d %d\n",$1,$2,$3}' ds_output.txt \
| sort -k2,2n -k3,3n | awk '{print $1}' | grep .png

- " > ../colroworderedfigs_000"
- " > ../colroworderedfigs_100"
- " > ../colroworderedfigs_200"

3. Repeat for all three figure directories.

4. Cat the 000 files into one.

cd ..
cat colroworderedfigs_000 colroworderedfigs_100 colroworderedfigs_200 > colroworderedfigs.txt

5. May have a problem with a duplicated file in DS_Store with and w/o spaces "Planes Cross Planes.png".
   
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

# Summary (148 files had spaces in their names - sheez)
- ___Figures 000 -> 8
- ___Figures 100 -> 77
- ___Figures 200 -> 63

