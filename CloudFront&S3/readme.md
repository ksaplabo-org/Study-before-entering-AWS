# CloudFrontとS3で静的サイトの構築

参考サイトは[こちら](https://qiita.com/sda134/items/74705085b5ab3de94463)

設定値						必須	Type
DistributionConfig						〇	DistributionConfig
    Aliases					-	Array of String
    CacheBehaviors					-	Array of CacheBehavior
        AllowedMethods				-	Array of String
        CachedMethods				-	Array of String
        CachePolicyId				条件による	String
        Compress				-	Boolean
        DefaultTTL				-	Number
        FieldLevelEncryptionId				-	String
        ForwardedValues				条件による	ForwardedValues
            Cookies			-	Cookies
                Forward		〇	String
                WhitelistedNames		条件による	Array of String
            Headers			-	Array of String
            QueryString			〇	Boolean
            QueryStringCacheKeys			-	Array of String
        FunctionAssociations				-	Array of FunctionAssociation
            EventType			-	String
            FunctionARN			-	String
        LambdaFunctionAssociations				-	Array of LambdaFunctionAssociation
            EventType			-	String
            IncludeBody			-	Boolean
            LambdaFunctionARN			-	String
        MaxTTL				-	Number
        MinTTL				-	Number
        OriginRequestPolicyId				-	String
        PathPattern				〇	String
        RealtimeLogConfigArn				-	String
        ResponseHeadersPolicyId				-	String
        SmoothStreaming				-	Boolean
        TargetOriginId				〇	String
        TrustedKeyGroups				-	Array of String
        TrustedSigners				-	Array of String
        ViewerProtocolPolicy				〇	String
    CNAMEs					-	Array of String
    Comment					-	String
    ContinuousDeploymentPolicyId					-	String
    CustomErrorResponses					-	Array of CustomErrorResponse
        ErrorCachingMinTTL				-	Number
        ErrorCode				〇	Integer
        ResponseCode				条件による	Integer
        ResponsePagePath				条件による	String
    CustomOrigin					-	LegacyCustomOrigin
        DNSName				〇	String
        HTTPPort				-	Integer
        OriginProtocolPolicy				〇	String
        OriginSSLProtocols				〇	Array of String
    DefaultCacheBehavior					〇	
        AllowedMethods				-	Array of String
        CachedMethods				-	Array of String
        CachePolicyId				条件による	String
        Compress				-	Boolean
        DefaultTTL				-	Number
        FieldLevelEncryptionId				-	String
        ForwardedValues				条件による	ForwardedValues
            Cookies			-	Cookies
                Forward		〇	String
                WhitelistedNames		条件による	Array of String
            Headers			-	Array of String
            QueryString			〇	Boolean
            QueryStringCacheKeys			-	Array of String
        FunctionAssociations				-	Array of FunctionAssociation
            EventType			-	String
            FunctionARN			-	String
        LambdaFunctionAssociations				-	Array of LambdaFunctionAssociation
            EventType			-	String
            IncludeBody			-	Boolean
            LambdaFunctionARN			-	String
        MaxTTL				-	Number
        MinTTL				-	Number
        OriginRequestPolicyId				-	String
        RealtimeLogConfigArn				-	String
        ResponseHeadersPolicyId				-	String
        SmoothStreaming				-	Boolean
        TargetOriginId				〇	String
        TrustedKeyGroups				-	Array of String
        TrustedSigners				-	Array of String
        ViewerProtocolPolicy				〇	String
    DefaultRootObject					-	String
    Enabled					〇	Boolean
    HttpVersion					-	String
    IPV6Enabled					-	Boolean
    Logging					-	Logging
        Bucket				〇	String
        IncludeCookies				-	Boolean
        Prefix				-	String
    OriginGroups					条件による	OriginGroups
        Items				-	Array of OriginGroup
            FailoverCriteria			〇	OriginGroupFailoverCriteria
                StatusCodes		〇	StatusCodes
                    Items	〇	Array of Integer
                    Quantity	〇	Integer
            Id			〇	String
            Members			〇	OriginGroupMembers
                Items		〇	Array of OriginGroupMember
                    OriginId	〇	String
                Quantity		〇	Integer
        Quantity				〇	Integer
    Origins					条件による	Array of Origin
        ConnectionAttempts				-	Integer
        ConnectionTimeout				-	Integer
        CustomOriginConfig				条件による	CustomOriginConfig
            HTTPPort			-	Integer
            HTTPSPort			-	Integer
            OriginKeepaliveTimeout			-	Integer
            OriginProtocolPolicy			〇	String
            OriginReadTimeout			-	Integer
            OriginSSLProtocols			-	Array of String
        DomainName				〇	String
        Id				〇	String
        OriginAccessControlId				-	String
        OriginCustomHeaders				-	OriginCustomHeaders
            HeaderName			〇	String
            HeaderValue			〇	String
        OriginPath				-	String
        OriginShield				-	OriginShield
            Enabled			-	Boolean
            OriginShieldRegion			-	String
        S3OriginConfig				条件による	S3OriginConfig
            OriginAccessIdentity			-	String
    PriceClass					-	String
    Restrictions					-	Restrictions
        GeoRestriction				〇	GeoRestriction
            Locations			条件による	Array of String
            RestrictionType			〇	String
    S3Origin					-	LegacyS3Origin
        DNSName				〇	String
        OriginAccessIdentity				-	String
    Staging					-	Boolean
    ViewerCertificate					-	ViewerCertificate
        AcmCertificateArn				条件による	String
        CloudFrontDefaultCertificate				条件による	Boolean
        IamCertificateId				条件による	String
        MinimumProtocolVersion				条件による	String
        SslSupportMethod				条件による	String
    WebACLId					-	String
Tags						-	Array of Tag
    Key					〇	String
    Value					〇	String
