# QueriesJPA


## DTO com ResultTransformer e createNativeQuery


  List postDTOs = entityManager
  .createNativeQuery(
      "select " +
      "       p.id as \"id\", " +
      "       p.title as \"title\" " +
      "from Post p " +
      "where p.created_on > :fromTimestamp")
      .setParameter( "fromTimestamp", Timestamp.from(LocalDateTime.of( 2016, 1, 1, 0, 0, 0 ).toInstant( ZoneOffset.UTC ) ))
      .unwrap( org.hibernate.query.NativeQuery.class )
      .setResultTransformer( Transformers.aliasToBean( PostDTO.class ) )
      .getResultList();
  
  
  
    Query query = entityManager.createNativeQuery("SELECT codigo \"codigo\", nome  \"nome\", endereco \"endereco\", tel1 \"tel1\" FROM clientes WHERE nome LIKE 'A%'", ClienteMOD.class);
    query.unwrap(SQLQueryImpl.class).setResultTransformer(new AliasToBeanResultTransformer(ClienteMOD.class));
    return (List<ClienteMOD>) query.getResultList();
  
  
  
  
