# Team Member Grid Style Guide

This document explains how to recreate the team member grid style with its features.

## Structure Overview
The design consists of a responsive grid of team member cards with hover effects, LinkedIn integration, and gradient overlays.

## Required Resources
1. Fonts:
   - Inter (400, 500, 600, 700)
   - Archivo Expanded (400, 500, 600, 700)
   - Import via Google Fonts

2. Assets needed:
   - LinkedIn icon image
   - Team member photos (recommended size: at least 400px height)

## Implementation Steps

### 1. HTML Structure
Create a container with two grid sections:
```html
<div class="container">
    <div class="grid"></div>     <!-- Main team grid -->
    <div class="grid-2"></div>   <!-- Secondary team grid -->
</div>
```

### 2. JavaScript Data Structure
Create an array of team member objects with the following properties:
```javascript
const teamMembers = [
    {
        name: 'Member Name',
        title: 'Job Title',
        email: 'email@domain.com',
        img: 'path/to/image.jpg',
        linkedin: 'https://linkedin.com/profile'
    }
    // Add more members...
];
```

### 3. Card Generation
Use JavaScript to dynamically create cards:
```javascript
const createMemberCard = (member) => {
    const card = document.createElement('div');
    card.className = 'card';
    
    card.innerHTML = `
        <div class="card-image">
            <img src="${member.img}" alt="${member.name}">
            ${member.linkedin ? `
                <a href="${member.linkedin}" target="_blank" class="linkedin-icon">
                    <img src="path/to/linkedin-icon.png" alt="LinkedIn">
                </a>
            ` : ''}
        </div>
        <div class="card-content">
            <h3>${member.name}</h3>
            <p class="title">${member.title}</p>
            ${member.email ? `
                <p class="email">
                    <a href="mailto:${member.email}">${member.email}</a>
                </p>
            ` : ''}
        </div>
    `;
    return card;
};
```

### 4. Key CSS Features

#### Grid Layout
```css
.grid, .grid-2 {
    display: grid;
    grid-template-columns: repeat(6, 1fr);
    gap: 20px;
    padding: 20px;
}
```

#### Card Design
```css
.card {
    background: #1a1a1a;
    border-radius: 16px;
    border: 1px solid rgba(242, 242, 242, 0.7);
    height: 400px;
    position: relative;
}
```

#### Image Overlay Gradient
```css
.card-image::after {
    content: '';
    position: absolute;
    bottom: 0;
    left: 0;
    width: 100%;
    height: 70%;
    background: linear-gradient(to top, #111111 10%, transparent 100%);
    z-index: 2;
}
```

#### Name Gradient Effect
```css
.card h3 {
    background: linear-gradient(135deg, #FFA155 33%, #FF0028 48%);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
}
```

### 5. Responsive Breakpoints
```css
@media (max-width: 1200px) {
    .grid { grid-template-columns: repeat(4, 1fr); }
    .grid-2 { grid-template-columns: repeat(2, 1fr); }
}

@media (max-width: 768px) {
    .grid { grid-template-columns: repeat(2, 1fr); }
}

@media (max-width: 480px) {
    .grid { grid-template-columns: 1fr; }
    .grid-2 { grid-template-columns: repeat(2, 1fr); }
}
```

## Additional Notes
1. Images use object-fit: cover for consistent sizing
2. LinkedIn icons have hover opacity effect
3. Email links have subtle hover animations
4. Cards have a fixed height of 400px
5. Text colors are optimized for dark backgrounds
