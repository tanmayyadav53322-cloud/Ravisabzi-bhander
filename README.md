# रवि सब्ज़ी भंडार (Ravi Sabzi Bhandar)

Hindi + Hinglish सब्ज़ी delivery website। Static site (एक `index.html`) + Supabase backend।

## Files
- `index.html`: पूरी website (Supabase से जुड़ी हुई)
- `supabase/schema.sql`: database, security rules और photo bucket
- `preview/`: Claude preview वाला पुराना version (Supabase के बिना)
- `netlify.toml`: Netlify settings

## Setup
1. **Database:** अगर नया Supabase project है तो Supabase → SQL Editor में `supabase/schema.sql` run करें। (मौजूदा project `hvvclavnemptsgaehrlb` में यह पहले से लगा है, दोबारा run न करें।)
2. **Keys:** `index.html` में सबसे ऊपर `SB_URL` और `SB_KEY` हैं। यहाँ सिर्फ़ **publishable** key रखें। `service_role` / secret key कभी नहीं।
3. **Host:** इस folder को Netlify Drop (app.netlify.com/drop), Vercel, Cloudflare Pages या GitHub Pages पर डालें।
4. **Owner पासवर्ड:** पहले Supabase → Authentication → Sign In / Providers में **Confirm email बंद** करें। फिर site खोलकर 👤 → "पहली बार? पासवर्ड बनाएँ" (कम से कम 8 अक्षर)। Login में email नहीं माँगा जाता; अंदर एक fixed खाता (`OWNER_EMAIL`, index.html में सबसे ऊपर) इस्तेमाल होता है। पहला खाता मालिक बनता है, इसलिए यह सबसे पहले करें।
   - पासवर्ड भूलने पर: Supabase → Authentication → Users से उस खाते का पासवर्ड बदलें।
5. **Sign-up बंद करें:** पासवर्ड बन जाने के बाद उसी जगह "Allow new users to sign up" बंद करें।
6. **दुकान की location:** Admin → दुकान की सेटिंग में Latitude और Longitude भरें। इनके बिना ऑर्डर नहीं लगेगा।
7. एक test सब्ज़ी जोड़ें और एक test ऑर्डर देकर देखें।

## Security
- Price, stock और delivery charge server (`place_order`) पर निकलते हैं, browser के भेजे दाम नहीं माने जाते।
- Orders सिर्फ़ मालिक पढ़ सकता है। Customer अपने ऑर्डर private token से देखता है।
- Products और settings सिर्फ़ मालिक बदल सकता है (Row Level Security)।
