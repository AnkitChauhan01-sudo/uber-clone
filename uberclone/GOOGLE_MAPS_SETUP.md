# Google Maps API Setup Guide

## Step 1: Get Your API Key

1. Go to [Google Cloud Console](https://console.cloud.google.com/)
2. Create a new project or select an existing one
3. Navigate to **APIs & Services** → **Credentials**
4. Click **Create Credentials** → **API Key**
5. Copy your API key

## Step 2: Enable Required APIs

Enable the following APIs in Google Cloud Console:

1. **Maps JavaScript API** - For displaying maps
2. **Places API** - For address autocomplete
3. **Routes API** - For directions and route calculation
4. **Geocoding API** - For converting coordinates to addresses

To enable:
- Go to **APIs & Services** → **Library**
- Search for each API and click **Enable**

## Step 3: Restrict Your API Key (Recommended)

For security, restrict your API key:

1. Go to **APIs & Services** → **Credentials**
2. Click on your API key
3. Under **API restrictions**, select **Restrict key**
4. Select these APIs:
   - Maps JavaScript API
   - Places API
   - Routes API
   - Geocoding API
5. Under **Application restrictions**, you can:
   - **HTTP referrers (web sites)**: Add your domain (e.g., `https://your-app.vercel.app/*`)
   - Or leave unrestricted for development

## Step 4: Add API Key to Your Application

### For Local Development

Create a `.env.local` file in the root directory:

```env
NEXT_PUBLIC_GOOGLE_MAPS_API_KEY=your_api_key_here
```

### For Vercel Deployment

1. Go to your Vercel project dashboard
2. Navigate to **Settings** → **Environment Variables**
3. Add a new variable:
   - **Name**: `NEXT_PUBLIC_GOOGLE_MAPS_API_KEY`
   - **Value**: Your API key
   - **Environment**: Production, Preview, Development (select all)
4. Click **Save**
5. Redeploy your application

## Step 5: Verify the Setup

After setting up the API key:

1. Visit your application
2. Check the browser console for any Google Maps errors
3. Test the map functionality:
   - The map should load on the dashboard
   - Address autocomplete should work
   - Route calculation should work

## How the API Key is Used

The application uses the Google Maps API key in the following way:

```typescript
import { setOptions, importLibrary } from '@googlemaps/js-api-loader';

setOptions({
  key: process.env.NEXT_PUBLIC_GOOGLE_MAPS_API_KEY || '',
  v: 'weekly',
});

await importLibrary('places');
await importLibrary('routes');
```

This is equivalent to using `key=API_KEY` parameter in the traditional script tag approach.

## Troubleshooting

### "This page can't load Google Maps correctly"
- Check if the API key is set correctly
- Verify the API key has the required APIs enabled
- Check browser console for specific error messages

### "RefererNotAllowedMapError"
- Add your domain to the HTTP referrer restrictions in Google Cloud Console
- Or temporarily remove restrictions for testing

### Maps not loading
- Verify `NEXT_PUBLIC_GOOGLE_MAPS_API_KEY` is set in environment variables
- Check that the key starts with `AIza...`
- Ensure billing is enabled in Google Cloud Console (free tier available)

## Billing

Google Maps API has a free tier:
- $200 free credit per month
- After that, pay-as-you-go pricing applies
- Monitor usage in Google Cloud Console

## Security Best Practices

1. **Restrict API key** to specific APIs and domains
2. **Use environment variables** - never commit API keys to git
3. **Monitor usage** regularly in Google Cloud Console
4. **Set up billing alerts** to avoid unexpected charges
5. **Rotate keys** periodically for security

