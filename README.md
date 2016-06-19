# B Plus Tree ( In Memory )
  Using C++, visualstudio2015, in windows10
  
  
# Insert Part
  template <class KEY, class DATA, class COMP, class EE>
bool BTree<KEY,DATA,COMP,EE>::insert( const KEY& key, const DATA& data )
{
    // if NULL root
    if( NULL == root ){
        // make B_Terminal_Node
        root = static_cast<B_Node<KEY,DATA,COMP,EE>*>( new B_Terminal_Node<KEY,DATA,COMP,EE>( fanout ) );
        first_node = static_cast<B_Terminal_Node<KEY,DATA,COMP,EE>*>( root );
        last_node = first_node;
    }
    // find Terminal B_Node
    //cout << "will find tnTemp.." << endl;
    B_Terminal_Node<KEY,DATA,COMP,EE>* tnTemp = findB_Terminal_Node( key, root );
    //cout << "finded tnTemp.." << endl;
    // temp for copyUp
    B_Internal_Node<KEY,DATA,COMP,EE>* inTemp = NULL;
    // insert
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
	if (isOk) {
		count++;
	}
    return isOk;
}
