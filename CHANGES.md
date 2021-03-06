
As of 3.0.0:

* API changes
  * SQLStore implementations no longer create or use a 'settings'
    table
  * SRegResponse.fromSuccessResponse returns None when no signed
    arguments were found
  * Added functions to generate request/response HTML forms with
    auto-submission javascript
      * Consumer (relying party) API: AuthRequest.htmlMarkup
      * Server API: server.OpenIDResponse.toHTML
  * PAPE (Provider Authentication Policy Extension) module
      * Updated extension for specification draft 2
      * Request.fromSuccessResponse returns None if PAPE response
        arguments were not signed

* New features
  * Demo server now supports OP-driven identifier selection
  * Demo consumer now has a "stateless" option
  * Fetchers now only read/request first megabyte of response

* Bug fixes
  * NOT NULL constraints were added to SQLStore tables where
    appropriate
  * message.fromPostArgs: use query.items() instead of iteritems(),
    fixes #161 (Affects Django users)
  * check_authentication requests: copy entire response, not just
    signed fields.  Fixes missing namespace in check_authentication
    requests
  * Consumer._verifyDiscoveryResults: fall back to OpenID 1.0 type if
    1.1 endpoint cannot be found; fixes discovery verification bug for
    certain OpenID 1 identifiers
  * SQLStore._execSQL: convert unicode arguments to str to avoid
    postgresql api bug with unicode objects (Thanks to Marek Kuziel.)
  * MySQLStore: Use ENGINE instead of TYPE when creating tables
  * server.OpenIDResponse.toFormMarkup: Use return_to from the
    request, not the response fields (Not all responses (i.e. cancel,
    setup_needed) include a return_to field.)
  * server.AssociationRequest.answer: include session_type in
    no-encryption assoc responses
  * OpenIDServiceEndpoint.getDisplayIdentifier: Don't include the
    fragment in display identifiers.
