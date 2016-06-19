# B Plus Tree ( In Memory )
  Using C++, visualstudio2015, in windows10
  
  
# Insert Core Part
    bool isOk = tnTemp->insert( key, data );
    if( isOk && tnTemp->isOver() )
    {
        inTemp = tnTemp->copyUp();

        if( last_node == tnTemp ) { last_node = tnTemp->Right(); }

        while( inTemp->isOver() )
        {
            inTemp = inTemp->moveUp();
        }
        if( !isRoot( inTemp ) && inTemp->isRoot() ) /// canRoot??
        {
            // now new Root!!
            setRoot( inTemp );
        }
    }

