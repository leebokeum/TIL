### 서블릿 기반 웹프로젝트에 ant를 추가하여 build.xml을 만들었다.

``` xml
<?xml version="1.0"?>

<project default="main" basedir="." name="ILDONG_OPEN_BOARD">
	<!--퍼로퍼티 파일 지정 -->
	<property file="build.properties" />
	<!--퍼로퍼티 설정 : 각종 폴더 & 생성파일 -->
	<property name="src.dir" value="../src" />
	<property name="web.dir" value="../WebContent" />
	<property name="dist.dir" value="dist" />
	<property name="build.dir" value="build" />
	<property name="war.file" value="${dist.dir}/ildong_board.war" />
	<!-- 컴파일에 필요한 라이브러리 패스를 설정한다. -->
	<!-- 컴파일 패스 설정 : 웹 라이브러리 위치 (WEB-INF/lib), 톰캣 라이브러리 추가(tomcat/lib) -->
	<path id="project.classpath">
		<pathelement location="${web.dir}/WEB-INF/lib" />
		<fileset dir="${web.dir}/WEB-INF/lib">
			<include name="*.jar" />
		</fileset>
	</path>

	<!-- 빌드 날짜를 스탬프로 찍는다 -->
	<target name="datentime" description="create current date">
		<tstamp>
			<format property="DSTAMP" pattern="yyyy-MM-dd" />
			<format property="TSTAMP" pattern="HH:mm:ss" />
		</tstamp>
		<echo message="Build started at : ${DSTAMP} - ${TSTAMP}" />
	</target>

	<!-- 빌드하기전에 빌드폴더 생성 및 WebContent?내의 파일을 build 폴더로 복사한다. -->
	<target name="prepare" depends="datentime, clean" description="copy web contents">
		<mkdir dir="${build.dir}" />
		<mkdir dir="${build.dir}/WEB-INF" />
		<mkdir dir="${build.dir}/WEB-INF/classes" />
		<copy todir="${build.dir}">
			<fileset dir="${web.dir}" />
		</copy>
	</target>

	<!-- build와 dist 폴더를 삭제한다. -->
	<target name="clean" description="delete build, dist">
		<delete dir="${dist.dir}" />
		<delete dir="${build.dir}" />
	</target>

	<!-- build 폴더에 자바 컴파일 후 classes 파일을 복사한다. -->
	<target name="build" depends="prepare" description="compile java">
		<javac srcdir="${src.dir}" destdir="${build.dir}/WEB-INF/classes" debug="${compile.debug}" deprecation="${compile.deprecation}" optimize="${compile.optimize}" classpathref="project.classpath" encoding ="UTF-8">
		</javac>
		<copy todir="${build.dir}/WEB-INF/classes">
			<fileset dir="${src.dir}" excludes="**/*.java, **/*.properties" />
		</copy>
	</target>

	<!--build 폴더를 프로젝트이름.war로 압축해서 dist 폴더로-->
	<target name="dist" depends="build" description="make war file from build to dist">
		<mkdir dir="${dist.dir}" />
		<jar destfile="${war.file}" basedir="${build.dir}" />
	</target>

    <target name="main" >
            <wsgen/>
    </target>
</project>
```

### 윈도우에서 실행할 때.
- ant 설치 후 환경 설정
``` shell
ant dist
```
