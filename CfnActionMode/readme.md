# CloudFormationのデプロイ時のActionModeについて

必須パラメータ		
CloudFormationのアクションモード		
1. Create or update a stack (スタックの作成または更新):		
    CREATE_UPDATE	
        指定されたスタックが存在しない場合、新しいスタックを作成します。
        既存のスタックがある場合、そのスタックを更新します。
        
2. Create or replace a change set (変更セットの作成または置換):		
    CHANGE_SET_REPLACE	
        変更セットが存在しない場合、新しい変更セットを作成します。
        既存の変更セットがある場合、それを削除して新しい変更セットを作成します。
        
3. Execute a change set (変更セットの実行):		
    CHANGE_SET_EXECUTE	
        既存の変更セットを実行します。
        
4. Delete a stack (スタックの削除):		
    DELETE_ONLY	
        指定されたスタックを削除します。存在しないスタックを指定した場合、アクションは正常に終了します。
        
5. Replace a failed stack (失敗したスタックの置換):		
    REPLACE_ON_FAILURE	
        指定されたスタックが存在しない場合、新しいスタックを作成します。
        既存のスタックが失敗状態（ROLLBACK_COMPLETE、ROLLBACK_FAILED、CREATE_FAILED、DELETE_FAILED、UPDATE_ROLLBACK_FAILED）にある場合、そのスタックを削除して新しいスタックを作成します。
        
