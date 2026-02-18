# SafeLayer Frontend

> Risk analysis dashboard for BNB Chain. Check the risk profile of any wallet or smart contract before you interact.

## Features

- **Real-time Risk Scoring**: AI-powered analysis with evidence-based scoring
- **Multi-Panel Analysis**:
  - Overview: Quick risk assessment
  - Evidence Panel: Detailed risk factors
  - Formula Breakdown: How risk score is calculated
  - On-Chain Indicators: Real-time blockchain data
  - Holder Analysis: Token holder distribution
  - Audit Panel: Contract audit status
  - GitHub Panel: Open source verification
  - Registry Status: On-chain proof verification

- **Dark Mode**: Built-in light/dark theme support
- **Responsive Design**: Mobile, tablet, and desktop optimized
- **Ambient Animations**: Smooth, performance-optimized UI

## Tech Stack

- **Framework**: Next.js 14 (React 18)
- **Language**: TypeScript 5.9
- **Styling**: Tailwind CSS 3
- **Charts**: Recharts for data visualization
- **Icons**: Lucide React
- **Testing**: Jest + React Testing Library
- **Deployment**: Vercel

## Quick Start (Local)

```bash
# Install dependencies
npm ci

# Create .env.local file
cp .env.example .env.local
# Edit .env.local:
# NEXT_PUBLIC_BACKEND_URL=http://localhost:3001

# Start development server
npm run dev

# Open browser
open http://localhost:3000
```

Environment variables required:
```
NEXT_PUBLIC_BACKEND_URL=http://localhost:3001
# Public only - safe to expose to browser
```

## Build & Production

```bash
# Production build
npm run build

# Start production server
npm start

# Type checking
npm run type-check
```

## Deployment

### Vercel (Recommended)

1. **Create Vercel Account**: https://vercel.com
2. **Import Project**:
   - New Project → Import Git Repository
   - Select `safelayer-frontend`
   - Vercel auto-detects Next.js
3. **Set Environment Variables** before deployment:
   ```
   NEXT_PUBLIC_BACKEND_URL = https://safelayer-backend.up.railway.app
   ```
   (Replace with your Railway backend URL)
4. **Deploy**: Click Deploy button → Wait 2 minutes
5. **Get URL**: Vercel provides production URL (e.g., `https://safelayer.vercel.app`)
6. **Update Backend CORS**: Go to Railway and update `CORS_ORIGIN=your-vercel-url`

### Configuration Files

- **`vercel.json`**: Vercel deployment config
  - Builds Next.js with optimizations
  - Sets security headers (X-Content-Type-Options, X-Frame-Options, etc.)
  - Region: Singapore (sin1)
- **`.env.example`**: Template for environment variables

## Project Structure

```
app/
├── layout.tsx          # Root layout with header/footer
├── page.tsx            # Main dashboard (client component)
└── globals.css         # Global styles + animations

components/
├── RiskAnalyzer.tsx    # Main analyzer/search component
├── RiskCard.tsx        # Risk score display card
├── EvidencePanel.tsx   # Detailed risk factors
├── FormulaBreakdown.tsx# How score is calculated
├── RadarChart.tsx      # Risk profile visualization
├── OnChainIndicatorsTable.tsx  # Blockchain metrics
├── HolderAnalysisPanel.tsx     # Token holder data
├── AuditPanel.tsx      # Audit status
├── GitHubPanel.tsx     # Open source info
├── RegistryStatus.tsx  # On-chain proof
├── DigitalNetworkBackground.tsx # Ambient animation
├── LogoAnimation.tsx   # Header logo animation
└── ... (utility components)

lib/
├── types.ts            # TypeScript interfaces
└── utils.ts            # Helper functions
```

## Features in Detail

### Risk Analysis Flow

1. User enters BNB Chain address
2. Frontend calls backend `/api/risk/:address`
3. Backend runs 5 parallel analysis modules
4. Results returned with breakdown by module
5. Recommendation displayed (safe/review/caution/high-risk)

### Risk Factors

- **Contract Scanner**: Code quality, patterns, security issues
- **Behavior Analyzer**: Transaction history, holder patterns
- **Scam Database**: Known scam list matching
- **Wallet History**: Holder age, distribution
- **Transparency**: Open source code availability

### Recommendations

- **Safe**: Risk score 0-30, low risk
- **Review**: Risk score 31-60, moderate risk
- **Caution**: Risk score 61-80, elevated risk
- **High Risk**: Risk score 81-100, very high risk

## Testing

```bash
# Run all tests
npm test

# Watch mode
npm test -- --watch

# Coverage
npm test -- --coverage
```

## Performance

- **Static generation**: Home page pre-rendered for instant loads
- **Image optimization**: Next.js automatic image optimization
- **Code splitting**: Route-based code splitting
- **CSS optimization**: Tailwind CSS purging unused styles
- **Animations**: GPU-accelerated CSS transforms

## Security

- ✅ XSS protection: React escapes by default
- ✅ CSRF protection: API uses SameSite cookies
- ✅ Security headers: X-Content-Type-Options, X-Frame-Options, CSP
- ✅ HTTPS only: Enforced in production
- ✅ Environment variables: Public vars only (NEXT_PUBLIC_)

## Troubleshooting

### Backend connection error?
- Check `NEXT_PUBLIC_BACKEND_URL` is correct
- Verify backend is running: `curl $BACKEND_URL/health`
- Check CORS: Backend must allow frontend origin

### Styles not loading?
- Clear `.next` folder: `rm -rf .next`
- Rebuild: `npm run build`
- Restart: `npm run dev`

### Hydration errors?
- CSS classes in `globals.css` are properly namespaced
- All dynamic content uses `'use client'` directive
- No server-only components in client components

## Browser Support

- Chrome 90+
- Firefox 88+
- Safari 14+
- Edge 90+

## Mobile Optimization

- Responsive grid layout
- Touch-friendly buttons (minimum 48px)
- Optimized font sizes for small screens
- Swipe support for panels

## Community & Support

- **GitHub Issues**: Report bugs or request features
- **Documentation**: See [DEPLOY.md](../DEPLOY.md) for full deployment guide
- **Backend Repo**: https://github.com/maniknur/safelayer-backend

## License

MIT

---

**Live URL** (after deployment): https://safelayer.vercel.app

**Backend API**: https://safelayer-backend.up.railway.app

**Smart Contract**: 0x20B28a7b961a6d82222150905b0C01256607B5A3 (BNB Testnet)
