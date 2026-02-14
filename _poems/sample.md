---
title: "सूरदास का पद"
author: "सूरदास"
language: "ब्रज"
---

मैया मोरी मैं नहीं माखन खायो।

<span class="dict-word" data-meaning="भोला, सरल">भोलो</span> भालो <span class="dict-word" data-meaning="मुख, चेहरा">मुख</span> देखि लीजै दधि मुख लेपु लगायो।

<span class="dict-word" data-meaning="खीर, चावल की मिठाई">खरिक</span> खरिक की ओट तू <span class="dict-word" data-meaning="रो रहा है">कहति</span> रोवति तू मोसों खीझि खिझायो।
```

5. **Scroll down and click "Commit changes"** → **"Commit changes"** again

---

## **STEP 6: Create the Layout for Poems (This Makes Dictionary Work!)**

This is the magical part that makes words clickable!

1. **Click "Add file" → "Create new file"** again

2. **In the "Name your file..." box, type:**
```
   _layouts/poem.html

<!DOCTYPE html>
<html lang="hi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{{ page.title }} - Kavya-Mimamsa</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Noto+Sans+Devanagari:wght@400;600&display=swap');
        
        body {
            font-family: 'Noto Sans Devanagari', sans-serif;
            max-width: 800px;
            margin: 0 auto;
            padding: 20px;
            line-height: 2;
            font-size: 18px;
        }
        
        .poem-header {
            border-bottom: 2px solid #333;
            padding-bottom: 20px;
            margin-bottom: 30px;
        }
        
        h1 {
            color: #8B4513;
            font-size: 32px;
        }
        
        .poem-content {
            background: #fef9f3;
            padding: 30px;
            border-radius: 8px;
            line-height: 2.5;
        }
        
        .dict-word {
            color: #2563eb;
            text-decoration: underline dotted;
            cursor: pointer;
            position: relative;
        }
        
        .dict-word:hover {
            color: #1e40af;
            background-color: #eff6ff;
        }
        
        .meaning-popup {
            display: none;
            position: absolute;
            background: white;
            border: 2px solid #2563eb;
            padding: 10px 15px;
            border-radius: 6px;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
            z-index: 1000;
            min-width: 200px;
            font-size: 16px;
            top: 100%;
            left: 50%;
            transform: translateX(-50%);
            margin-top: 5px;
        }
        
        .meaning-popup::before {
            content: '';
            position: absolute;
            top: -8px;
            left: 50%;
            transform: translateX(-50%);
            width: 0;
            height: 0;
            border-left: 8px solid transparent;
            border-right: 8px solid transparent;
            border-bottom: 8px solid #2563eb;
        }
    </style>
</head>
<body>
    <div class="poem-header">
        <h1>{{ page.title }}</h1>
        <p><strong>रचयिता:</strong> {{ page.author }}</p>
        <p><strong>भाषा:</strong> {{ page.language }}</p>
    </div>
    
    <div class="poem-content">
        {{ content }}
    </div>
    
    <script>
        // Clickable dictionary functionality
        document.querySelectorAll('.dict-word').forEach(word => {
            // Create popup element
            const popup = document.createElement('div');
            popup.className = 'meaning-popup';
            popup.textContent = word.getAttribute('data-meaning');
            word.appendChild(popup);
            
            // Show on click
            word.addEventListener('click', function(e) {
                e.stopPropagation();
                // Hide all other popups
                document.querySelectorAll('.meaning-popup').forEach(p => {
                    if (p !== popup) p.style.display = 'none';
                });
                // Toggle this popup
                popup.style.display = popup.style.display === 'block' ? 'none' : 'block';
            });
        });
        
        // Hide popup when clicking outside
        document.addEventListener('click', function() {
            document.querySelectorAll('.meaning-popup').forEach(p => {
                p.style.display = 'none';
            });
        });
    </script>
</body>
</html>
