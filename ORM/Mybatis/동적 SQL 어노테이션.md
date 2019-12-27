### MyBatis에서는 동적 SQL 어노테이션을 지원한다.
- @SelectProvider
- @InsertProvider
- @UpdateProvider
- @DeleteProvider

*sql 문을 DB에 저장하여 String 형으로 불러오고 Provider들을 이용하여 class와 실행할 메소드를 불러와서 쿼리를 실행할 수 있다.
xml 수정 후 서버를 다시 내렸다 올릴 필요 없이 바로 DB의 sql 문을 수정하면 바로 서버에 반영이 되는 장점이 있다. 
다이나믹 쿼리를 사용하지 못하는 제약 상황이 있지만, sql문을 바꿀수 있다.*

~~~ java
public interface ExcelMapper {
    @SelectProvider(type = DynamicProvider.class, method = "getDynamicQuery")
    @Options(fetchSize = 500)
    @ResultType(LinkedHashMap.class)
    void dynamicQueryForList(String query, ResultHandler rs) throws Exception;
    //options annotiation으로 fetch size 조절 가능
    //mybatis 바로 이용하기!
    //ResultHandler 사용하게 변수 받아옴

}

public class DynamicProvider {
    public String getDynamicQuery(String query) {
        return query;
    }
}
~~~