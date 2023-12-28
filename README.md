# GL sales Transactions ETL

### Queries

Select

    --FactGLTran
    gl.FactGLTranID,
    gl.JournalID,
    gl.GLTranDescription,
    gl.GLTranAmount,
    gl.GLTranDate,

    --dimGLAcct
    gla.AlternateKey AS 'GLAcctNum',
    gla.GLAcctName,
    gla.[Statement],
    gla.Category,
    gla.Subcategory,

    --Dimstore
    gls.AlternateKey AS 'StoreNum',
    gls.StoreName,
    gls.ManagerID,
    gls.PreviousManagerID,
    gls.ContactTel,
    gls.AddressLine1, 
    gls.AddressLine2,
    gls.ZipCode,

    --dimregion
    glr.AlternateKey as RegionNum,
    glr.RegionName,
    glr.SalesRegionName,

    --LastRefreshDates
    CONVERT(datetime2, GETDATE() at time zone 'UTC' at time zone 'Central Standard Time') AS 'LastRefreshDate'

    FROM FactGLTran AS gl
    INNER JOIN dimGLAcct AS gla ON gl.GLAcctID = gla.GLAcctID
    INNER JOIN dimStore AS gls ON gl.StoreID = gls.StoreID
    INNER Join dimRegion AS glr ON gls.RegionID =glr.RegionID

