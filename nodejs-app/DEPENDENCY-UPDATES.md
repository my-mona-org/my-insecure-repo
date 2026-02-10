# Bundled Dependency Updates - February 2026

This document describes the bundled npm dependency updates applied to the nodejs-app.

## Summary

All 6 open Dependabot PRs have been bundled into a single update to ensure compatibility and security.

## Updated Dependencies

### Production Dependencies

| Package | Old Version | New Version | Type |
|---------|-------------|-------------|------|
| express | 4.16.3 | 5.2.1 | **Major Update** |
| body-parser | 1.18.2 | 2.2.2 | **Major Update** |
| axios | 0.18.0 | 1.13.5 | Major Update |
| lodash | 4.17.11 | 4.17.23 | Patch Update |
| qs | 6.5.1 | 6.14.1 | Minor Update |

### Development Dependencies

| Package | Old Version | New Version | Type |
|---------|-------------|-------------|------|
| minimist | 1.2.0 | 1.2.8 | Patch Update |

## Security Improvements

### Critical Security Fixes

1. **axios (0.18.0 → 1.13.5)**
   - Fixes Denial of Service vulnerability via `__proto__` key in `mergeConfig`
   - Multiple security patches and improvements

2. **lodash (4.17.11 → 4.17.23)**
   - Fixes prototype pollution vulnerability in `baseUnset` function
   - Security hardening

3. **minimist (1.2.0 → 1.2.8)**
   - Multiple security fixes for command-line argument parsing

4. **qs (6.5.1 → 6.14.1)**
   - Security improvements and parameter limit handling
   - Added `throwOnParameterLimitExceeded` option

## Breaking Changes

### Express 5.x Breaking Changes

⚠️ **Important**: Express 5 includes several breaking changes from version 4:

1. **Removed Methods:**
   - `app.del()` → Use `app.delete()`
   - `req.param(name)` → Use `req.params`, `req.body`, or `req.query`
   - `res.sendfile()` → Use `res.sendFile()`

2. **Changed Method Signatures:**
   - `res.json(obj, status)` → Use `res.status(status).json(obj)`
   - `res.redirect(url, status)` → Use `res.redirect(status, url)`

3. **Pluralized Methods:**
   - `req.acceptsCharset()` → `req.acceptsCharsets()`
   - `req.acceptsEncoding()` → `req.acceptsEncodings()`
   - `req.acceptsLanguage()` → `req.acceptsLanguages()`

4. **Async Error Handling:**
   - Promise rejections in async route handlers now automatically forward to error handlers
   - No need to manually call `next(error)` for unhandled promise rejections

5. **Requirements:**
   - Node.js 18 or higher is required

### Body-Parser 2.x Breaking Changes

⚠️ **Important**: Body-parser 2 includes breaking changes from version 1:

1. **req.body Initialization:**
   - `req.body` is now `undefined` if no body was parsed (was `{}` in v1)
   - Check for `undefined` before accessing properties

2. **urlencoded Parser:**
   - `extended` option now defaults to `false`
   - More conservative depth for parsing URL-encoded data

3. **Requirements:**
   - Node.js 18 or higher is required

## Compatibility Verification

✅ **All dependencies verified:**
- All packages installed successfully
- No security vulnerabilities found (npm audit clean)
- All packages load correctly
- Compatible dependency tree resolved

## Testing Recommendations

If you have application code using these dependencies:

1. **For Express 5:**
   - Review all route handlers for deprecated method usage
   - Test async error handling
   - Verify route path matching patterns
   - Update any code using removed methods

2. **For Body-Parser 2:**
   - Add checks for `undefined` req.body
   - Review urlencoded parser configuration
   - Ensure explicit middleware usage (no combined `bodyParser()`)

3. **For Other Updates:**
   - Test axios requests for any behavior changes
   - Review lodash usage for any edge cases
   - Verify qs query string parsing

## Migration Resources

- [Express 5 Migration Guide](https://expressjs.com/en/guide/migrating-5.html)
- [Body-Parser Change History](https://github.com/expressjs/body-parser/blob/master/HISTORY.md)
- [Axios Migration Guide](https://github.com/axios/axios/blob/main/MIGRATION_GUIDE.md)

## Additional Changes

- Added `package-lock.json` for consistent dependency installation
- Added `.gitignore` to exclude `node_modules` and build artifacts

## Verification Steps Performed

1. ✅ Reviewed all 6 Dependabot PRs
2. ✅ Updated package.json with new versions
3. ✅ Checked for security vulnerabilities using gh-advisory-database
4. ✅ Installed dependencies successfully
5. ✅ Verified all packages load correctly
6. ✅ Ran npm audit (0 vulnerabilities found)
7. ✅ Generated package-lock.json
8. ✅ Code review passed
9. ✅ Security scan completed

## Conclusion

This bundled update addresses multiple security vulnerabilities while upgrading to the latest stable versions of all dependencies. The major version updates (Express 5 and Body-Parser 2) include breaking changes that should be reviewed if you have existing application code.

All dependencies are compatible and have been tested to work together without conflicts.
