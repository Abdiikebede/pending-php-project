<?php
/**
 * PENDING PROJECT CLONER - All-in-One
 * One-click full project duplicator
 * Author: Abdi Kebede
 * Email: abdikebede17@gmail.com
 */

// ==================== CONFIGURATION ====================
$source = __DIR__ . DIRECTORY_SEPARATOR . 'pending_project';
$destination = __DIR__ . DIRECTORY_SEPARATOR . 'cloned_project_' . date('Y-m-d_H-i-s');
$exclude = ['node_modules', 'vendor', '.git', 'cache', 'logs', 'tmp'];
// =======================================================

// Colors for CLI output
$colors = [
    'red' => "\033[31m",
    'green' => "\033[32m",
    'yellow' => "\033[33m",
    'blue' => "\033[34m",
    'magenta' => "\033[35m",
    'cyan' => "\033[36m",
    'reset' => "\033[0m"
];

// Detect if running in terminal
$isCLI = (php_sapi_name() === 'cli');

function colorize($text, $color, $colors, $isCLI) {
    if (!$isCLI) return $text;
    return $colors[$color] . $text . $colors['reset'];
}

// Display banner
function showBanner($colors, $isCLI) {
    $banner = "
    ╔══════════════════════════════════════════════════════════╗
    ║                                                          ║
    ║     🚀 PENDING PROJECT CLONER - All-in-One v1.0         ║
    ║                                                          ║
    ║     Instantly duplicate any project with one click!     ║
    ║                                                          ║
    ╚══════════════════════════════════════════════════════════╝
    ";
    echo colorize($banner, 'cyan', $colors, $isCLI) . "\n";
}

// Copy directory recursively
function copyDirectory($source, $destination, $exclude, $colors, $isCLI) {
    if (!is_dir($source)) {
        echo colorize("❌ Error: Source directory not found: $source\n", 'red', $colors, $isCLI);
        return false;
    }
    
    if (!is_dir($destination)) {
        mkdir($destination, 0777, true);
    }
    
    $dir = opendir($source);
    $filesCopied = 0;
    $totalSize = 0;
    
    while ($file = readdir($dir)) {
        if ($file == "." || $file == "..") continue;
        
        $sourcePath = $source . DIRECTORY_SEPARATOR . $file;
        $destPath = $destination . DIRECTORY_SEPARATOR . $file;
        
        // Check exclude patterns
        $shouldExclude = false;
        foreach ($exclude as $pattern) {
            if (strpos($sourcePath, $pattern) !== false) {
                $shouldExclude = true;
                break;
            }
        }
        
        if ($shouldExclude) {
            echo colorize("  ⏭️  Skipped: $file\n", 'yellow', $colors, $isCLI);
            continue;
        }
        
        if (is_dir($sourcePath)) {
            echo colorize("  📁 Entering: $file\n", 'blue', $colors, $isCLI);
            $result = copyDirectory($sourcePath, $destPath, $exclude, $colors, $isCLI);
            $filesCopied += $result['files'];
            $totalSize += $result['size'];
        } else {
            copy($sourcePath, $destPath);
            $size = filesize($sourcePath);
            $totalSize += $size;
            $filesCopied++;
            echo colorize("  📄 Copied: $file (" . formatSize($size) . ")\n", 'green', $colors, $isCLI);
        }
    }
    closedir($dir);
    
    return ['files' => $filesCopied, 'size' => $totalSize];
}

// Format file size
function formatSize($bytes) {
    if ($bytes >= 1073741824) {
        return number_format($bytes / 1073741824, 2) . ' GB';
    } elseif ($bytes >= 1048576) {
        return number_format($bytes / 1048576, 2) . ' MB';
    } elseif ($bytes >= 1024) {
        return number_format($bytes / 1024, 2) . ' KB';
    } else {
        return $bytes . ' bytes';
    }
}

// Create a simple HTML report
function createReport($source, $destination, $stats) {
    $html = <<<HTML
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Clone Report - Pending Project Cloner</title>
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }
        .report-card {
            background: white;
            border-radius: 20px;
            padding: 40px;
            max-width: 600px;
            width: 100%;
            box-shadow: 0 20px 60px rgba(0,0,0,0.3);
            animation: slideIn 0.5s ease-out;
        }
        @keyframes slideIn {
            from {
                opacity: 0;
                transform: translateY(-30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }
        h1 {
            color: #667eea;
            margin-bottom: 10px;
            font-size: 2em;
        }
        .success-icon {
            font-size: 60px;
            text-align: center;
            margin-bottom: 20px;
        }
        .stats {
            background: #f7f9fc;
            border-radius: 10px;
            padding: 20px;
            margin: 20px 0;
        }
        .stat-item {
            display: flex;
            justify-content: space-between;
            padding: 10px 0;
            border-bottom: 1px solid #e1e8ed;
        }
        .stat-item:last-child {
            border-bottom: none;
        }
        .stat-label {
            font-weight: bold;
            color: #555;
        }
        .stat-value {
            color: #667eea;
            font-weight: bold;
        }
        .path {
            background: #f0f0f0;
            padding: 15px;
            border-radius: 8px;
            font-family: monospace;
            font-size: 12px;
            word-break: break-all;
            margin: 15px 0;
        }
        .btn {
            display: inline-block;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 12px 24px;
            text-decoration: none;
            border-radius: 8px;
            margin-top: 20px;
            transition: transform 0.3s;
        }
        .btn:hover {
            transform: translateY(-2px);
        }
        .footer {
            text-align: center;
            margin-top: 30px;
            color: #888;
            font-size: 12px;
        }
    </style>
</head>
<body>
    <div class="report-card">
        <div class="success-icon">✅</div>
        <h1 style="text-align: center;">Clone Successful!</h1>
        <p style="text-align: center; color: #666; margin-bottom: 20px;">Your project has been duplicated successfully</p>
        
        <div class="stats">
            <div class="stat-item">
                <span class="stat-label">📁 Files Copied</span>
                <span class="stat-value">{$stats['files']}</span>
            </div>
            <div class="stat-item">
                <span class="stat-label">💾 Total Size</span>
                <span class="stat-value">{$stats['size_formatted']}</span>
            </div>
            <div class="stat-item">
                <span class="stat-label">⏱️ Duration</span>
                <span class="stat-value">{$stats['duration']} seconds</span>
            </div>
        </div>
        
        <div class="path">
            <strong>📂 Source:</strong> {$source}<br>
            <strong>🎯 Destination:</strong> {$destination}
        </div>
        
        <div style="text-align: center;">
            <a href="{$destination}" class="btn">📁 Open Cloned Project</a>
        </div>
        
        <div class="footer">
            <p>Pending Project Cloner • Created by Abdi Kebede</p>
            <p>abdikebede17@gmail.com</p>
        </div>
    </div>
</body>
</html>
HTML;
    
    file_put_contents($destination . DIRECTORY_SEPARATOR . 'clone_report.html', $html);
    return 'clone_report.html';
}

// ==================== MAIN EXECUTION ====================

showBanner($colors, $isCLI);

echo colorize("\n📂 Source: ", 'yellow', $colors, $isCLI) . $source . "\n";
echo colorize("🎯 Destination: ", 'yellow', $colors, $isCLI) . $destination . "\n\n";

// Check if source exists
if (!file_exists($source)) {
    echo colorize("\n❌ ERROR: 'pending_project' folder not found!\n", 'red', $colors, $isCLI);
    echo colorize("\n📝 Please create a folder named 'pending_project' and put your project inside it.\n", 'yellow', $colors, $isCLI);
    echo colorize("\nExample structure:\n", 'cyan', $colors, $isCLI);
    echo colorize("  /your-folder/\n", 'cyan', $colors, $isCLI);
    echo colorize("    ├── clone.php (this file)\n", 'cyan', $colors, $isCLI);
    echo colorize("    └── pending_project/\n", 'cyan', $colors, $isCLI);
    echo colorize("        └── (your project files here)\n\n", 'cyan', $colors, $isCLI);
    exit(1);
}

$startTime = microtime(true);

echo colorize("🔄 Cloning in progress...\n\n", 'cyan', $colors, $isCLI);

$result = copyDirectory($source, $destination, $exclude, $colors, $isCLI);

$endTime = microtime(true);
$duration = round($endTime - $startTime, 2);

echo colorize("\n" . str_repeat("═", 50) . "\n", 'magenta', $colors, $isCLI);
echo colorize("✅ CLONE COMPLETED SUCCESSFULLY!\n", 'green', $colors, $isCLI);
echo colorize(str_repeat("═", 50) . "\n", 'magenta', $colors, $isCLI);
echo colorize("📁 Files copied: ", 'yellow', $colors, $isCLI) . $result['files'] . "\n";
echo colorize("💾 Total size: ", 'yellow', $colors, $isCLI) . formatSize($result['size']) . "\n";
echo colorize("⏱️  Time taken: ", 'yellow', $colors, $isCLI) . $duration . " seconds\n";
echo colorize("🎯 Location: ", 'yellow', $colors, $isCLI) . $destination . "\n";
echo colorize(str_repeat("═", 50) . "\n", 'magenta', $colors, $isCLI);

// Create HTML report
$stats = [
    'files' => $result['files'],
    'size' => $result['size'],
    'size_formatted' => formatSize($result['size']),
    'duration' => $duration
];
$reportFile = createReport($source, $destination, $stats);
echo colorize("\n📄 HTML report created: " . $destination . DIRECTORY_SEPARATOR . $reportFile . "\n", 'cyan', $colors, $isCLI);

if ($isCLI) {
    echo colorize("\n💡 Quick tip: To clone again, just run 'php clone.php'\n", 'yellow', $colors, $isCLI);
} else {
    echo "<br><br><a href='$destination/clone_report.html'>View Clone Report</a>";
}

echo "\n";
?>
