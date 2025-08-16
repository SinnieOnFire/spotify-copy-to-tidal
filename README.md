# Spotify to Tidal Playlist Transfer Tool

A robust Python tool for transferring playlists from Spotify to Tidal with advanced track matching capabilities, including enhanced support for Japanese/CJK music content.

## Features

- **Smart Track Matching**: Uses fuzzy string matching with multiple strategies for accurate track identification
- **CJK Character Support**: Enhanced matching for Japanese, Korean, and Chinese music with romanization handling
- **Session Persistence**: Saves authentication tokens to avoid repeated logins
- **Rate Limiting**: Intelligent rate limiting with exponential backoff to respect API limits
- **Detailed Reporting**: Comprehensive transfer statistics with language-specific success rates
- **Missing Track Export**: Automatically exports unmatched tracks with search suggestions
- **Batch Processing**: Handles large playlists efficiently with progress tracking
- **Error Recovery**: Robust error handling with retry logic for network issues

## Perfect For

- **International Music Collections**: Optimized matching for multi-language content
- **Large Playlists**: Handles hundreds of tracks with progress reporting
- **Music Migration**: Moving your entire music library between streaming services
- **Cross-Platform Sync**: Maintaining playlists across multiple streaming services

## Requirements

- Python 3.8 or higher
- Spotify Premium account (for API access)
- Tidal subscription
- Spotify Developer App credentials

## Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/spotify-to-tidal-transfer.git
   cd spotify-to-tidal-transfer
   ```

2. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

3. **Set up Spotify API credentials**
   - Go to [Spotify Developer Dashboard](https://developer.spotify.com/dashboard/applications)
   - Create a new app
   - Note your **Client ID** and **Client Secret**
   - Add `http://127.0.0.1:8080` as a redirect URI in your app settings

## Configuration

1. **Edit the script** and replace the placeholder credentials:
   ```python
   SPOTIFY_CLIENT_ID = "your_actual_client_id_here"
   SPOTIFY_CLIENT_SECRET = "your_actual_client_secret_here"
   ```

2. **Alternative: Use environment variables** (recommended for security):
   ```bash
   export SPOTIFY_CLIENT_ID="your_client_id"
   export SPOTIFY_CLIENT_SECRET="your_client_secret"
   ```

## Usage

1. **Run the script**
   ```bash
   python spotify_to_tidal_transfer.py
   ```

2. **Follow the prompts**
   - Authenticate with Spotify (browser will open)
   - Authenticate with Tidal (browser will open)
   - Select a playlist to transfer
   - Confirm and wait for completion

## Example Output

```
Transfer completed!
Playlist: My Music Collection (from Spotify)
Total tracks: 186
Successfully transferred: 117
Not found: 69
Success rate: 62.9%

Success by language:
Japanese/CJK tracks: 37/79 (46.8%)
Latin/English tracks: 80/107 (74.8%)

Missing tracks exported to: missing_tracks_My_Music_Collection_20250816_100029.txt
```

## Advanced Features

### Smart Matching Strategies
- **Multiple search variants**: Original, normalized, romanized versions
- **Fuzzy matching**: Handles slight differences in track titles and artist names
- **Language-aware thresholds**: Different matching strictness for different character sets
- **Text normalization**: Removes common prefixes, suffixes, and formatting variations

### Session Management
- **Token persistence**: Automatically saves and reuses authentication tokens
- **Session validation**: Verifies saved sessions before use
- **Cross-platform compatibility**: Works on Windows, macOS, and Linux

### Error Handling
- **Exponential backoff**: Automatically handles rate limiting
- **Retry logic**: Recovers from temporary network issues
- **Graceful degradation**: Continues processing even if some tracks fail

## Missing Track Export

When tracks cannot be found on Tidal, the tool exports a detailed report with:

- **Search suggestions** for each missing track
- **Cleaned titles** (removing parentheses, brackets, etc.)
- **Romanized versions** for CJK tracks
- **Voice actor names** extracted from character songs
- **Alternative search strategies**

## Configuration Options

You can customize the matching behavior by modifying these settings in the code:

```python
self.match_threshold = 80          # Minimum similarity score (0-100)
self.cjk_match_threshold = 70      # Lower threshold for CJK tracks
self.max_search_results = 15       # Number of search results to analyze
```

## Known Limitations

- **Tidal API limitations**: Some authentication methods may vary by region
- **Licensing restrictions**: Some tracks may not be available on Tidal in your region
- **CJK romanization**: Multiple romanization systems may affect matching accuracy
- **Rate limiting**: Large playlists may take significant time to process

## Troubleshooting

### Spotify Authentication Issues
- Ensure redirect URI is exactly `http://127.0.0.1:8080`
- Check that your Spotify app has the correct client ID/secret
- Try clearing browser cookies for Spotify

### Tidal Authentication Issues
- Make sure you're logged into Tidal in your browser
- Clear browser cache and cookies for Tidal
- Try running the script again after a few minutes

### Low Match Rates
- Adjust `match_threshold` for stricter/looser matching
- Check the exported missing tracks file for manual search suggestions
- Consider that some content may not be available on Tidal

## Contributing

Contributions are welcome! Please feel free to submit pull requests or open issues for:

- Bug fixes and improvements
- Additional streaming service support
- Enhanced matching algorithms
- Better CJK language support
- Documentation improvements

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Disclaimer

This tool is for personal use only. Please respect the terms of service of both Spotify and Tidal. The authors are not responsible for any violations of streaming service terms or any data loss during the transfer process.
