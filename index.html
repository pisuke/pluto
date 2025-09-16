// --- CONFIGURATION ---
// ⬇️ PASTE YOUR GOOGLE SHEET "PUBLISH TO WEB" CSV URL HERE
// (See instructions above on how to get this)
// const googleSheetURL = 'https://docs.google.com/spreadsheets/d/e/1d1-A0E-D-2qFXeiykmID6NacWsVbwhlvuoSShq-saTI/pub?gid=0&single=true&output=csv';
const googleSheetURL = 'https://docs.google.com/spreadsheets/d/e/2PACX-1vR3ZhUCybmE8wlpt3Z1zjNVDllGPV7-QJKaK-65bfFklq0meb65QcgOUGFebFYr8ThuHNazvjraHDtB/pub?gid=0&single=true&output=csv'

// This is the header name in your sheet that holds the asset name
// It IS case-sensitive and must match your CSV header exactly.
const assetNameColumn = 'name'; // e.g., 'assetname'
// ---------------------


let video;
let sheetData; // This will be a p5.Table object
let scanningEnabled = true;

// DOM Elements
let statusElement;
let linksContainer;

// Load the Google Sheet data before the sketch starts
function preload() {
  // Use loadTable() for CSV data.
  // 'csv' = specify the format
  // 'header' = specify that the first row is a header
  sheetData = loadTable(googleSheetURL, 'csv', 'header');
  // print(sheetData);
  // print(sheetData.getColumn('assetname'));
}

function setup() {
  let canvas = createCanvas(400, 300);
  // canvas.parent('main'); // Attach canvas to the <main> element
  
  // Forces the pixel array to be 1:1 with the canvas size
  pixelDensity(1);
  // -----------------------
  
  // Initialize webcam
  video = createCapture(VIDEO);
  video.size(width, height);
  video.hide(); // Hide the extra HTML5 video element

  // Get references to our HTML elements
  statusElement = select('#status');
  linksContainer = select('#links-container');

  // Check if data loaded
  if (sheetData && sheetData.getRowCount() > 0) {
    console.log('Google Sheet CSV data loaded successfully.');
    console.log('Columns found:', sheetData.columns);
  } else {
    statusElement.html('Error: Could not load Google Sheet data. Check URL and publishing permissions.');
    scanningEnabled = false;
  }
}

function draw() {
  if (scanningEnabled) {
    
    // NEW, ROBUST CHECK:
    // We check video.width (the video element's *intrinsic* width).
    // This value is 0 until the webcam stream is fully initialized
    // and has delivered its metadata.
    if (video.width > 0) {
      
      // Only draw the video and try to scan if the webcam is ready
      image(video, 0, 0, width, height);
      findQRCode();

    } else {
      // Optional: Show a "loading" message while we wait
      background(0);
      fill(255);
      textAlign(CENTER, CENTER);
      text("Waiting for webcam...", width / 2, height / 2);
    }
  }
}

function findQRCode() {
  // Load the pixels from the CANVAS (not the video element)
  loadPixels();
  
  // Safety check: If the pixels array is empty,
  // skip this frame. This prevents the "Malformed data" error.
  if (pixels.length === 0) {
    return;
  }

  // Pass the canvas's pixel data to jsQR
  const code = jsQR(pixels, width, height, {
    inversionAttempts: 'dontInvert',
  });

  if (code) {
    // --- QR Code Found! ---
    scanningEnabled = false; // Stop scanning
    let assetDataString = code.data;
    let assetData = JSON.parse(assetDataString);
    print(assetData);
    statusElement.html(`✅ Code Found: ${assetDataString}`);
    
    print(assetData.asset.name);
    
    // Now, process this asset name
    processAssetName(assetDataString);
  }
}

function processAssetName(assetDataString) {
  if (!sheetData) {
    linksContainer.html('<p>Error: No sheet data to process.</p>');
    return;
  }

  const rows = sheetData.getRows();
  let matchingRow = null;
  let assetData = JSON.parse(assetDataString);
  let assetName = assetData.asset.name;

  // Look for the matching asset name in the sheet data
  for (let row of rows) {
    // Use .getString(columnName) to get the value
    const sheetAssetName = row.getString(assetNameColumn);

    if (sheetAssetName === assetName) {
      matchingRow = row;
      break;
    }
  }

  // --- Display the Results ---
  if (matchingRow) {
    // Found a match! Clear the links container.
    linksContainer.html(''); 
    
    // Get all column names from the table
    const columns = sheetData.columns;
    
    // Iterate over all column names
    for (let colName of columns) {
      // We want to skip the asset name column itself
      if (colName !== assetNameColumn) {
        
        // Get the link URL from the matching row by its column name
        let linkURL = matchingRow.getString(colName);
        let linkName = colName; // The column name is the link name
        
        // Make sure it's a valid link before creating an anchor tag
        if (linkURL && (linkURL.startsWith('http://') || linkURL.startsWith('https://'))) {
          let linkElement = createA(linkURL, `${linkName}: ${linkURL}`);
          linkElement.parent(linksContainer);
          linkElement.attribute('target', '_blank'); // Open in new tab
        } else if (linkURL) {
          // If it's not a link but has data, just display it as text
          let textElement = createP(`${linkName}: ${linkURL}`);
          textElement.parent(linksContainer);
        }
        // If linkURL is empty or null, we simply skip it.
      }
    }
  } else {
    // No match found
    linksContainer.html(`<p>❌ Asset "${assetName}" not found in the Google Sheet.</p>`);
  }
  
  // Add a "Scan Again" button
  let resetButton = createButton('Scan Another Code');
  resetButton.parent(linksContainer);
  resetButton.mousePressed(() => {
    // Reset the sketch
    scanningEnabled = true;
    statusElement.html('Point a QR code at the camera.');
    linksContainer.html('<p>Scan a code to see related links here.</spp>');
    resetButton.remove();
  });
}