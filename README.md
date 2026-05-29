🚀 Pending Project Cloner — One-Click Full Project Duplicator
⚡ Instantly duplicate any PHP (or any language) project with a single command!
No manual copying • No missing files • No broken paths — just run and done!

https://img.shields.io/badge/PHP-8.0%252B-777BB4?style=for-the-badge&logo=php&logoColor=white
https://img.shields.io/badge/Platform-Windows%2520%257C%2520Linux%2520%257C%2520macOS-blue?style=for-the-badge
https://img.shields.io/badge/License-Free%2520to%2520Use-brightgreen?style=for-the-badge
https://img.shields.io/badge/Version-1.0.0-orange?style=for-the-badge

✨ Perfect For
<table> <tr> <td>
✅ Backups
✅ Staging Environments
✅ Code Reviews
✅ Deployment Preparation
✅ Safe Experiments
✅ Team Handoffs

</td> <td align="center"> <br/> 🎯 <b>One Command</b><br/> ⚡ <b>One Second</b><br/> 🔄 <b>100% Perfect Copy</b> </td> </tr> </table>
🤔 Why This Tool?
When you're working on a "pending" project and need to:

Scenario	Manual Way	This Tool
Test risky changes	😰 Copy 100+ files	✅ 1 second
Show progress to supervisor	😫 Zip & extract	✅ 1 click
Deploy to staging	😓 FTP headache	✅ Run & done
Backup before refactoring	😬 Miss hidden files	✅ Complete clone
This script does it perfectly — every single time!

🌟 Features
Feature	Status	Emoji
Full recursive folder copy	✅ Done	📁
Preserves exact file structure	✅ Done	🎯
Creates missing directories	✅ Done	🏗️
Zero dependencies required	✅ Done	📦
Cross-platform (Win/Linux/Mac)	✅ Done	💻
Single command execution	✅ Done	⚡
Automatic error handling	✅ Done	🛡️
Progress indicators	✅ Done	📊
📦 What Gets Copied?
text
✅ All PHP files
✅ All HTML/CSS/JS files
✅ Images & assets
✅ Configuration files
✅ Hidden files (.env, .gitignore)
✅ Nested subdirectories (any depth)
❌ Nothing gets missed!
🚀 Quick Start Guide (3 Seconds Setup)
Step 1: Download
bash
git clone https://github.com/yourusername/pending-project-cloner.git
# OR just download the ZIP
Step 2: Prepare
bash
# Place your existing project inside:
pending_project/
Step 3: Run
bash
php one_time_copy.php
Step 4: Done! 🎉
text
Your cloned project is ready at:
cloned_project/
📋 Example Usage
bash
# Before running
my_projects/
├── pending_project/     # Your original project
│   ├── index.php
│   ├── css/
│   ├── js/
│   └── uploads/

# Run the command
$ php one_time_copy.php

# After running
my_projects/
├── pending_project/     # Original (unchanged)
└── cloned_project/      # Perfect duplicate!
    ├── index.php
    ├── css/
    ├── js/
    └── uploads/
🛠️ Command Line Options
bash
# Basic usage
php one_time_copy.php

# Specify custom source/destination
php one_time_copy.php --source=my_project --dest=my_backup

# With verbose output
php one_time_copy.php --verbose
📁 Project Structure
text
pending-project-cloner/
│
├── one_time_copy.php      # Main cloner script
├── pending_project/       # Put your project here
│   └── (your files)
├── cloned_project/        # Output folder (auto-created)
├── README.md              # This file
└── .gitignore             # Git ignore rules
💡 Pro Tips
<details> <summary><b>🔧 Tip 1: Create a backup before major changes</b></summary>
bash
php one_time_copy.php
# Make risky changes in 'cloned_project'
# Original stays safe in 'pending_project'
</details><details> <summary><b>🎨 Tip 2: Create multiple variations</b></summary>
bash
# Copy and experiment
php one_time_copy.php
# Modify cloned_project
# Run again for another copy!
</details><details> <summary><b>⚡ Tip 3: Add to your PATH for global access</b></summary>
bash
# Add alias to .bashrc or .zshrc
alias clone-project='php /path/to/one_time_copy.php'
</details>
❓ Frequently Asked Questions
Q: Does it work with databases?
A: Only files — for DB, export SQL separately.

Q: Will it overwrite existing files?
A: No, it creates a timestamped backup or asks for confirmation.

Q: Can I use this for non-PHP projects?
A: Absolutely! Works with any language — Python, Node.js, React, etc.

Q: Is it safe for large projects (10,000+ files)?
A: Yes, it handles large directories efficiently.

🔄 Compatibility
OS	Status	Tested Version
Windows 10/11	✅	PHP 8.2
Linux (Ubuntu)	✅	PHP 8.0+
macOS	✅	PHP 8.1+
WSL	✅	Any version
🐛 Troubleshooting
Issue	Solution
"Permission denied"	Run with sudo/administrator
"Source folder not found"	Check pending_project exists
Memory exhausted	Increase memory_limit in php.ini
🗺️ Roadmap
Add ZIP compression option

Add exclude patterns (node_modules, vendor)

Add sync mode (update only changed files)

Add GUI version

Add progress bar for large files

🤝 Contributing
Contributions welcome! Feel free to:

🐛 Report bugs

💡 Suggest features

🔧 Submit pull requests

📄 License
Free to use — no restrictions!
Use it personally, commercially, or modify as needed.

📬 Contact
Abdi Kebede
📧 abdikebede17@gmail.com
🐙 GitHub: @yourusername

⭐ Show Your Support
If this tool saved you time, please:

⭐ Star this repo

🍴 Fork it

📢 Share with colleagues

<div align="center">
Built with ❤️ for developers who value their time

Report Bug · Request Feature · Star on GitHub

</div>
