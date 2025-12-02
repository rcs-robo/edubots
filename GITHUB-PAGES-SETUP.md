# GitHub Pages & Wiki Setup Instructions

This guide will help you set up GitHub Pages and Wiki for the EduBots repository.

## 📁 What's Been Created

### GitHub Pages Site (`docs/` folder)
- ✅ `docs/index.html` - Main landing page
- ✅ `docs/help.html` - Help & documentation page
- ✅ `docs/download.html` - Download page with instructions
- ✅ `docs/assets/css/style.css` - Modern, responsive stylesheet

### Wiki Templates (`wiki-templates/` folder)
- ✅ `Home.md` - Wiki home page with navigation
- ✅ `Installation-Guide.md` - Detailed installation instructions
- ✅ `NanoDiffBot-Guide.md` - Complete NanoDiffBot documentation

## 🚀 Step 1: Commit and Push to GitHub

First, commit all the new files to your repository:

```bash
cd /Users/harsh/Desktop/edubots

# Add all new files
git add docs/ wiki-templates/ GITHUB-PAGES-SETUP.md

# Commit
git commit -m "Add GitHub Pages site and Wiki templates

- Created responsive landing page with navigation
- Added comprehensive help and documentation page
- Added download page with installation instructions
- Created wiki templates for documentation
- Modern CSS styling with mobile support"

# Push to GitHub
git push origin main
```

## 🌐 Step 2: Enable GitHub Pages

1. Go to your repository on GitHub: https://github.com/rcs-robo/edubots

2. Click on **Settings** (top right, gear icon)

3. Scroll down to **Pages** section (left sidebar)

4. Under "Build and deployment":
   - **Source:** Select "Deploy from a branch"
   - **Branch:** Select `main` branch
   - **Folder:** Select `/docs`
   - Click **Save**

5. Wait 1-2 minutes for GitHub to build your site

6. Your site will be live at:
   ```
   https://rcs-robo.github.io/edubots/
   ```

7. You can also add a custom domain if you own one (optional)

## 📚 Step 3: Enable GitHub Wiki

1. In your repository, go to **Settings**

2. Scroll down to **Features** section

3. Check the box next to **Wikis**

4. Click **Save** (if there's a save button)

5. You should now see a **Wiki** tab at the top of your repository

## 📝 Step 4: Populate the Wiki

### Option A: Using GitHub Web Interface (Easiest)

1. Click the **Wiki** tab in your repository

2. Click **Create the first page** (or **New Page**)

3. Copy the content from `wiki-templates/Home.md` and paste it into the editor

4. Title the page: `Home`

5. Click **Save Page**

6. Repeat for other wiki pages:
   - Create "Installation-Guide" page from `Installation-Guide.md`
   - Create "NanoDiffBot-Guide" page from `NanoDiffBot-Guide.md`
   - Add more pages as needed

### Option B: Cloning Wiki as Git Repository (Advanced)

GitHub Wikis are actually git repositories:

```bash
# Clone the wiki
cd /Users/harsh/Desktop
git clone https://github.com/rcs-robo/edubots.wiki.git

# Copy template files
cd edubots.wiki
cp ../edubots/wiki-templates/*.md .

# Commit and push
git add .
git commit -m "Initial wiki content"
git push origin master
```

## ✅ Step 5: Verify Everything Works

### Check GitHub Pages
1. Visit: https://rcs-robo.github.io/edubots/
2. Test navigation between Home, Help, and Download pages
3. Check that all links work
4. Test on mobile device (should be responsive)

### Check Wiki
1. Visit: https://github.com/rcs-robo/edubots/wiki
2. Verify Home page content
3. Check links between wiki pages
4. Verify links to GitHub Pages work

## 🎨 Step 6: Customize (Optional)

### Update Colors
Edit `docs/assets/css/style.css` and change color variables:

```css
:root {
    --primary-color: #2563eb;    /* Change to your brand color */
    --secondary-color: #64748b;  /* Change to your accent color */
    --accent-color: #f59e0b;     /* Change to highlight color */
}
```

### Add Logo
1. Create or get your logo image
2. Save to `docs/assets/images/logo.png`
3. Update HTML files to use your logo:
   ```html
   <img src="assets/images/logo.png" alt="EduBots Logo">
   ```

### Update Content
- Edit HTML files in `docs/` to match your project details
- Update wiki pages with your specific information
- Add screenshots and images to wiki

## 📊 Step 7: Add to README

Update your `README.md` to link to the new pages:

```markdown
# EduBots

Educational robotics platform for block-based programming.

## 🌐 Resources

- **Website:** https://rcs-robo.github.io/edubots/
- **Documentation:** https://rcs-robo.github.io/edubots/help.html
- **Download:** https://rcs-robo.github.io/edubots/download.html
- **Wiki:** https://github.com/rcs-robo/edubots/wiki

## Quick Start

\`\`\`bash
docker run -d --name edubot -p 1999:1999 openroberta/lab
\`\`\`

Visit http://localhost:1999 to start programming!

See the [Installation Guide](https://github.com/rcs-robo/edubots/wiki/Installation-Guide) for detailed setup instructions.
```

## 🔧 Troubleshooting

### GitHub Pages not showing
- Check Settings → Pages to ensure it's enabled
- Make sure `docs/` folder is selected
- Wait 2-3 minutes after pushing changes
- Check GitHub Actions tab for build status
- Try accessing with https:// instead of http://

### Wiki not available
- Make sure Wikis are enabled in Settings → Features
- Check if your repository is public (wikis require public repos, or pro/team accounts for private)

### Broken links
- Relative links in wiki use format: `[Link Text](Page-Name)`
- Links to GitHub Pages from wiki: `[Link](https://rcs-robo.github.io/edubots/)`
- Links to wiki from Pages: `https://github.com/rcs-robo/edubots/wiki`

### CSS not loading
- Check file path in HTML: `href="assets/css/style.css"`
- Ensure files are in correct folders
- Clear browser cache
- Check browser console for 404 errors

## 📈 Next Steps

1. **Add more wiki pages:**
   - First-Program.md
   - Connecting-Your-Robot.md
   - Troubleshooting guides
   - Tutorial pages

2. **Add images:**
   - Robot photos
   - Wiring diagrams
   - Screenshot tutorials
   - Block programming examples

3. **Set up Google Analytics** (optional):
   - Add tracking code to HTML pages
   - Monitor page views
   - Understand user behavior

4. **Add search functionality:**
   - Wiki has built-in search
   - For Pages, can add Google Custom Search
   - Or implement Algolia DocSearch

5. **Enable discussions:**
   - Settings → Features → Discussions
   - Create Q&A, Ideas, and Help categories
   - Link from your Pages site

## 🎉 You're Done!

Your EduBots repository now has:
- ✅ Professional landing page
- ✅ Comprehensive documentation
- ✅ Download instructions
- ✅ Searchable wiki
- ✅ Mobile-responsive design
- ✅ Easy to maintain and update

Share your new URLs:
- **Website:** https://rcs-robo.github.io/edubots/
- **Wiki:** https://github.com/rcs-robo/edubots/wiki

---

Questions? Issues? [Open an issue on GitHub](https://github.com/rcs-robo/edubots/issues)
